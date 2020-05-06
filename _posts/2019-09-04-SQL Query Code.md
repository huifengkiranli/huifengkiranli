SQL Query Code

* Case:电商RFM MODEL

```mysql
# 新建表格，选取原表格部分字段
create table data1 
as select CustomerID,InvoiceNo,InvoiceDate,Quantity,UnitPrice,Country from UK_data;

# 统计缺失值null
select sum(case when CustomerID is null then 1 else 0 end) as 'sum_customerid',
       sum(case when InvoiceNo  is null then 1 else 0 end) as 'sum_invocieNo',
       sum(case when InvoiceDate is null then 1 else 0 end) as 'sum_invoiceDate',
       sum(case when Quantity    is null then 1 else 0 end) as 'sum_quantity',
       sum(case when UnitPrice   is null then 1 else 0 end) as 'sun_unitprice',
       sum(case when Country     is null then 1 else 0 end)as 'sum_country'
from data1;
# 创建新表，将null值的字段转为0
create table data2 
select coalesce(CustomerID,0)as CustomerID,InvoiceNo,InvoiceDate,Quantity,UnitPrice,Country from data1;

# 查找异常值 
select max(InvoiceDate),min(InvoiceDate), max(Quantity),min(Quantity),max(UnitPrice),min(UnitPrice)
from data2;
# 处理UnitPrice的异常值 
select * from data2 where UnitPrice <=0;
delete from data2 where UnitPrice <=0;

# 日期格式处理：新增日期列，格式化日期 str_to_date(),删除旧日期列 
alter table data2 add column InvoiceDatetime varchar(255) not NULL
update data2 set InvoiceDatetime = STR_TO_DATE(InvoiceDate,'%m/%d/%Y %H:%i')
alter table data2 drop InvoiceDate;

# 新增列Monetary 
alter table data2 add column Monetary float not NULL
update data2 set Monetary = Quantity*UnitPrice;

# 复制表格 
create table data3 like data2
insert into data3 select distinct* from data2 
select * from data3;

# RFM模型 
create table RFM 
as select CustomerID, MAX(InvoiceNo) as InvoiceNo,MAX(Quantity) as Quantity,MAX(UnitPrice) as UnitPrice,
MAX(Country) as Country,MAX(InvoiceDatetime) as InvoiceDatetime, 
DATEDIFF('2011-12-09',MAX(InvoiceDatetime)) as 'R',
count(DISTINCT InvoiceNo) as 'F',
round(SUM(Monetary),2) as 'M'
FROM data3
group by CustomerID, InvoiceNo,Quantity,UnitPrice,Country,InvoiceDatetime
ORDER BY R desc, F desc, M desc;

# RFM 评分表 
create table RFMscore as select *,
(case when R <=30 then 5
      when R >30 and R <=90 then 4
      when R >90 and R <= 180 then 3
      when R >180 and R <365 then 2 else 1 end) as 'Rscore',
(case when F >80 then 5
      when F >20 and F <=80 then 4
      when F >10 and F <=20 then 3
      when F >5 and F <=10 then 2 else 1 end) as 'Fscore',
(case when M > 10000 then 5
      when M > 5000 and M <= 10000 then 4
      when M >1000 and M <=5000 then 3
      when M >300 and M <= 1000 then 2 else 1 end) as 'Mscore'
from RFM;

# 求平均值 
select ROUND(AVG(Rscore),1) as Ravg,
       ROUND(AVG(Fscore),1) as Favg,
			 ROUND(AVG(Mscore),1) as Mavg from RFMscore;
		 
 # RFMvalue 计算分数
 create table RFMvalue as select *,
(case when Rscore > 3.8 then 1 else 0 end) as Rvalue,
(case when Fscore > 1.3 then 1 else 0 end) as Fvalue,
(case when Mscore > 2.0 then 1 else 0 end) as Mvalue from RFMscore;

# RFM 客户贴标签
create table RFMfinal as select *,
(case when Rvalue=1 and Fvalue=1 and Mvalue=1 then '重要价值客户' 
      when Rvalue=0 and Fvalue=1 and Mvalue=1 then '重要唤回客户'
      when Rvalue=1 and Fvalue=0 and Mvalue=1 then '重要深耕客户' 
      when Rvalue=1 and Fvalue=1 and Mvalue=0 then '潜力客户'
      when Rvalue=0 and Fvalue=0 and Mvalue=1 then '重要挽留客户' 
      when Rvalue=1 and Fvalue=0 and Mvalue=0 then '新客户' 
      when Rvalue=0 and Fvalue=1 and Mvalue=0 then '一般维持客户' 
  else '流失客户' end) as '客户分类'
	from RFMvalue;
```

* Case:AARRR model建立

```mysql
#用户总数量：对sessions表中的user_id进行group by，再统计数量,或者 count(distinct user_id)也可以。
SELECT COUNT(*)  AS 'user_amount'
FROM (SELECT user_id FROM sessions GROUP BY user_id) 
	as total_session;

#活跃用户的定义：用户操作产品大于等于10次。
SELECT COUNT(*)  AS 'active_user_amount'
FROM (SELECT user_id FROM sessions GROUP BY user_id 
HAVING COUNT(user_id) >= 10)
	as activation;

#注册用户：通过sessions表中的用户与注册用户表进行内关联，统计出已注册用户数量
SELECT COUNT(*) AS 'register_user_amount'
FROM (SELECT user_id FROM sessions GROUP BY user_id) as s
	INNER JOIN train_users_2 ON s.user_id = train_users_2.id;

#下单用户：用户行为中’reservations‘，统计“reservations”的用户（group by去重）。
SELECT COUNT(*) AS 'booking_user_amount'
FROM (SELECT user_id FROM sessions WHERE action_detail = 'reservations' 
	GROUP BY user_id) 
		as booking;

#实际支付用户：用户行为中'payment_instruments'，group by去重
SELECT COUNT(*) AS 'checkout_user_amount'
FROM (SELECT user_id FROM sessions WHERE action_detail = 'payment_instruments' 
	GROUP BY user_id) 
	as checkout;

#复购用户：用户行为‘payment_instruments’操作次数大于1次的用户，group by去重
SELECT COUNT(*) AS 'repurhcase_user_amount'
FROM (SELECT user_id FROM sessions WHERE action_detail = 'reservations' 
	GROUP BY user_id HAVING COUNT(user_id) >= 2) repurchase;
	
#新建表存储查询结果 
create table funnel (event VARCHAR (20) primary KEY, user_amount INT (10));

insert into funnel values ('Acquisition',135484),('Activation',114001),
	('Register',73815),('Booking',10367),('Checkout',9019),('Repurchase',5446);
```

* Case:定期存款客户用户画像

```mysql
# 查看数据总数 
select count(*) from bank;
# 概览数据 
desc bank; 
# 新增一列序号列, 设为primary key
alter table bank add id int(4) not null
primary key auto_increment first;
# 新增一列，为是否问题赋值1或0 
select *, case when (deposit='yes') then 1
else -1 end as mark 
from bank; 

# 有定期存款客户的年龄分层并计算比重
select case when age <20 then '<20' 
when age >=20 and age <30 then '[20,30)' 
when age >=30 and age <40 then '[30,40)' 
when age >=40 and age <60 then '[40,60)'
else '>60' end 
as 'age_group',
count(*), 
concat(round((count(age)/(select count(*) from bank2 ))*100,2),'%') as 'PER'  
from bank2
where deposit = 'yes'
group by case when age <20 then '<20' 
when age >=20 and age <30 then '[20,30)' 
when age >=30 and age <40 then '[30,40)' 
when age >=40 and age <60 then '[40,60)'
else '>60' end 
order by count(*) desc;
```

*  Case: LendingClub P2P贷款

```mysql
# 新增加一列序号列 
# 新增一列序号列, 设为primary key
alter table loan add id int(4) not null
primary key auto_increment first;
# 更改数据大小写
update loan set emp_title=UPPER(emp_title);
# 统计空值null项总数		
select sum(case when loan_amnt is null then 1 else 0 end) as 'sum_loan_amnt_null',
	sum(case when term is null then 1 else 0 end) as 'sum_term_null',
	sum(case when int_rate is null then 1 else 0 end) as 'sum_int_rate_null',
	sum(case when installment is null then 1 else 0 end) as 'sum_installment_null',
	sum(case when grade is null then 1 else 0 end) as 'sum_grade_null',
	sum(case when emp_title is null then 1 else 0 end) as 'sum_emp_title_null',
	sum(case when emp_length is null then 1 else 0 end ) as 'sum_emp_length_null',
	sum(case when home_ownership is null then 1 else 0 end) as 'sum_home_ownership_null',
	sum(case when annual_inc is null then 1 else 0 end) as 'sum_annual_inc_null',
	sum(case when loan_status is null then 1 else 0 end) as 'sum_loan_status_null',
	sum(case when purpose is null then 1 else 0 end) as 'sum_purpose_null',
	sum(case when addr_state is null then 1 else 0 end) 'sum_addr_state_null'
from loan; 
# 删除null记录，where条件
delete from loan where annual_inc is null;
```

* Window function_排名

```mysql
create table TEST_ROW_NUMBER_OVER(
       room_id varchar(10) not null,
       name varchar(10) null,
       age varchar(10) null,
       salary int null
);
select * from TEST_ROW_NUMBER_OVER;
insert into TEST_ROW_NUMBER_OVER(room_id,name,age,salary) values(1,'a',10,8000);
insert into TEST_ROW_NUMBER_OVER(room_id,name,age,salary) values(1,'a2',11,6500);
insert into TEST_ROW_NUMBER_OVER(room_id,name,age,salary) values(2,'b',12,13000);
insert into TEST_ROW_NUMBER_OVER(room_id,name,age,salary) values(2,'b2',13,4500);
insert into TEST_ROW_NUMBER_OVER(room_id,name,age,salary) values(3,'c',14,3000);
insert into TEST_ROW_NUMBER_OVER(room_id,name,age,salary) values(3,'c2',15,20000);
insert into TEST_ROW_NUMBER_OVER(room_id,name,age,salary) values(4,'d',16,30000);

# 在使用over等开窗函数时，over里头的分组及排序的执行晚于“where，group by，order by”的执行。
# ROW_NUMBER()按行排序号
select room_id, name, age, salary, row_number() over (order by salary desc) rn 
from TEST_ROW_NUMBER_OVER;

# over(partition by  order by) 分组排名
select room_id,name,age,salary,row_number()over(partition by room_id order by salary desc) rn 
from TEST_ROW_NUMBER_OVER;
# 全选分组后的排名，不能省略最后的t1
select  * from (
select room_id,name,age,salary,row_number() over(partition by room_id order by salary desc) rn 
from TEST_ROW_NUMBER_OVER
) t1;

# 每组salary排名第二名之前的：分组排名 over(partition by  order by)再选第一名
select  * from (
select room_id,name,age,salary,row_number() over(partition by room_id order by salary desc) rn 
from TEST_ROW_NUMBER_OVER
) t1
where t1.rn<2;

# 排名后，选出每组年龄在13-16岁之间的
select room_id,name,age,salary,row_number()over(order by salary desc) rn
from TEST_ROW_NUMBER_OVER t 
where t.age between '13' and '16';

# with as 用法 
with tabs as
(select room_id, name, age, salary, row_number()over(partition by room_id order by salary desc) rn
    from TEST_ROW_NUMBER_OVER t)
select * from tabs 
where rn=1;

# rank()over 同分同排名不跳跃
select room_id,name,age,salary,rank()over(order by salary desc) rk 
from TEST_ROW_NUMBER_OVER t;

# DENSE_RANK()over 同分同排名但跳跃
select room_id,name,age,salary, DENSE_RANK() over(order by salary desc) dr 
from TEST_ROW_NUMBER_OVER t;

# NTILE(4)分组函数，按salary分成4个组
select room_id,name,age,salary, NTILE(4) over(order by salary desc) rn
from TEST_ROW_NUMBER_OVER t;
'''
