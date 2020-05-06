SQL query code

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