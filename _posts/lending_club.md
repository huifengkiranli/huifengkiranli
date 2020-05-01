MySQL&Tableau:P2P贷款用户画像分析

# 一、分析背景

LendingClub是美国最大的P2P公司，定位是无担保的纯信息中介，利用互联网技术连接投资者和借款人，降低中介成本。作为无担保的P2P平台，LendingClub能吸引投资者依靠的是其成熟有效的信用分级模型——贷款逾期率及坏账率严格按借款人等级区分（信用等级越低，逾期率坏账率越高），Lending Club的风控模型也是值得更多的P2P公司学习和借鉴的。

# 二、分析目的

在互联网金融盛行的时代，客户信息尤为重要，能准确掌握客户信息，有清晰的用户画像，对金融产品的精准营销至关重要。而LendingClub作为P2P纯信息中介的鼻祖，值得我们深入研究。

# 三、分析思路

1. 客户自身客观维度

2. 客户与平台相关性维度

3. 需要深刻分析的问题：

1）客户居住地、职业、年收入、工作年限及房屋拥有情况分析；

2）平台中客户的评估等级、贷款目的及贷款金额利率情况分析；

3）相关性分析：信用等级与年收入关系分析、贷款目的与贷款金额关系分析。

# 四、Tableau分析报告
## 客户群特征：
- 集中在东南沿海地区，且多为工作十年以上的教师、经理等，收入水平大致集中在收入5-15万美元，并且大部分客户有按揭还贷的压力。

### 1. 工作年限及年收入
- 平台的主要客群工作年限为十年以上，两年和一年以下：十年以上工作年限的客户占比最大，达到35.39%，平均年收入最高；其次两年工作年限的客户（9.64%），占比明显低于前者；最后是一年以下工作年限的客户，占8.99%。
- 三类客户的平均年收入均高于七万美元，可见平台的客户还是比较优质。

![loant5](/Users/hui2046/Desktop/loant5.png)

### 2. 地域分布
- 客户占比最多的5个州分别是：加利福尼亚州（13.91%），纽约州（8.24%），德克萨斯州（8.24%），佛罗里达州（7.17%）和伊利诺斯州（4.03%）；
- 客户占比最小的两个州分别是：艾奥瓦州，爱荷华州。
- 可见，沿海经济比较发达的地区贷款需求比较高，特别是西部和南部及北部纽约，主要原因可能是，发达地区商业化水平高，人们的金融意识比较强，消费水平较高，资金也需求比较大。

![loant1](/Users/hui2046/Desktop/loant1.png)

### 3. 财产状况

- 房屋状况：近半数客户贷款买房（49.16%），有还房贷的经济压力；租房状态的客户达39.59%，自有房屋无贷款客户达到11.19%；
- 收入状况：有按揭贷款买房的客户平均年收入最高（88487美元），其次是自有房屋的客户，年收入约72890元，具备较好的经济条件；而第二大主体的租房客户年收入是66734美元，经济实力较弱。

![loant2](/Users/hui2046/Desktop/loant2.png)

### 4. 职业分布
- 职业分布：教师职业在申请贷款的客户中，占有最高的比例13.3%；第二高的是经理占比112.36%，接着是自有企业主。
- 职业与年收入：教师的平均年薪约65727美元，经理的平均年薪约79825美元，自有企业主年薪较高，92335美元。

![loant8](/Users/hui2046/Desktop/loant8.png)

### 5. 信用评级与年收入
- 大部分客户在平台的信用评级都较高，其中B类客户最多（29.35%），其次C类（28.75%），第三是A类客户占比19.15%；评级最低的G类客户仅占0.54%。
- 各类信用评级客户的年收入，A类客户最高 89999美元，其次是B类客户78930美元，最低年收入的是D类客户71168美元。

![loant4](/Users/hui2046/Desktop/loant4.png)

## 贷款产品偏好
### 1. 贷款目的及金额
-贷款目的：平台客户贷款目的为债务合并的达到56.53%，说明偿还其它贷款的占多数，为了偿还信用卡的客户占22.87%，第三大类是贷款用于改善家庭（6.66%）。
-贷款目的与贷款金额关系上：债务合并是贷款目的的客户平均15966美元，是最高的；偿还信用卡的客户平均贷款金额是15319美元，贷款金额最低的目的是旅游和教育，因为不是大额支出。

![loant6](/Users/hui2046/Desktop/loant6.png)
### 2. 贷款期限
- 平台一共两种期限的贷款产品，其中36个月的贷款客户达到71.21%,而60个月期限的贷款客户占比为28.79%。

![loant3](/Users/hui2046/Desktop/loant3.png)

### 3. 贷款金额及利率
-贷款金额：36个月期限的客户平均贷款金额为12745美元，60个月期限的贷款客户贷款金额约为20738美元。
-贷款利率：36个月期限贷款的平均利率为11.95%，60个月的平均利率为15.92%，期限越长利率越高。
![loant7](/Users/hui2046/Desktop/loant7.png)

## 总结与建议

### 客户自身维度：

- 客户在东南部和西部沿海经济比较发达的地区，可以加大对该地区客户的推广力度，尤其职业稳定的客户。

- 客户职业为教师、经理客户贷款占比较大，对这两类职业客户可以做客户等级分类进行标准化审核。

- 工作年限为10+，拥有自有住宅的客户可以放宽审核条件，对小于10年的，有按揭或租房的客户加强审核。

### 平台业务维度

- 客户信用等级为B/C的占比较大，可以再细化审核标准；

- 针对贷款目的为偿还其他债务的客户需要严格审核条件或要求其做一定的担保，以降低坏账风险。
- 产品期限过于单一，可以加强研究和开发新产品。


# 五、MySQL数据处理
## 查找缺失值

```mysql

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
```
![loan1](/Users/hui2046/Desktop/Screenshot 2020-05-01 at 13.37.09.png)

notes: 一共有数据2260668条，其中字段'emp_title 职业名称'缺失值有166934，保留为null作分析；'annul_inc'年收入字段有4条空值，比例不大，直接删除。

```mysql
delete from loan where annual_inc is null;
```
## 查询异常值
```mysql

select max(loan_amnt),min(loan_amnt),max(term),min(term),
			max(int_rate),min(int_rate),max(emp_length),min(emp_length) from loan;
```

![loan2](/Users/hui2046/Desktop/loan2.png)

notes: 没有需要处理的异常值

# 分析数据
## loan_amnt 贷款金额

```mysql

select loan_amnt,count(*) from loan
group by loan_amnt
order by count(*) desc;
```
![loan3](/Users/hui2046/Desktop/loan3.png)

notes: 贷款金额选择最好的是$10,000,占比8.28%，其次是$20,000 (5.79%).

```mysql
select grade,avg(loan_amnt) from loan
group by grade
order by avg(loan_amnt) desc;
```
![loan4](/Users/hui2046/Desktop/loan4.png)

notes: 所有客户的平均贷款金额为15046.95美元, 而风险评级分数最低的G类客户平均贷款金额最高（20383.98美元), 其次是F类客户（19124.64美元），ABC三类客户平均贷款金额均小于总的平均贷款金额。

## term 贷款期限

```mysql
select term, avg(loan_amnt),count(*) from loan
group by term 
order by term asc;
```
![loan5](/Users/hui2046/Desktop/loan5.png)

notes: 贷款期限有36个月和60个月，71%的客户选择的是36个月，36个月的贷款里平均贷款金额是12745美元，低于总平均贷款金额；60个月平均贷款金额高于总平均贷款金额，期限越长，贷款金额越高。

## 利率，每月分期还款金额，年收入

```mysql 

select grade,round(avg(int_rate),2),round(avg(installment),2),round(avg(annual_inc),2)
from loan
group by grade 
order by grade asc;
```
![loan6](/Users/hui2046/Desktop/loan6.png)

notes: 风险评估得分高A的客户，贷款利率最低7.08%，平均年收入最高89902美元.

## 工作年限，年收入，贷款金额，贷款利率分析

```mysql
select emp_length,count(emp_length),round(avg(loan_amnt),2),round(avg(int_rate),2),round(avg(annual_inc),2)
from loan
group by emp_length 
order by emp_length desc;
```
![loan7](/Users/hui2046/Desktop/loan7.png)
notes: 可见贷款人数最多的是有10年以上工作年限的 (33.08%)，其次是两年（9%）和三年（8%）工作年限的；10年以上工作年限的客户平均贷款金额是最高16242.19美元，平均年收入也是最高86566.15美元. 

## 职业，贷款金额和年收入分析

```mysql
select emp_title,count(emp_title),round(avg(loan_amnt),2),round(avg(annual_inc),2)
from loan 
group by emp_title 
order by count(emp_title) desc
limit 20;
```
![loan10](/Users/hui2046/Desktop/loan10.png)
notes: 客户职业中，申请贷款最多的职业是教师（2.04%），平均年收入为65699美元；其次是第二多的职业是经理（1.89%），平均年收入是79804美元。

## 房屋所有权，年收入和贷款金额分析

```mysql
select home_ownership,count(home_ownership),round(avg(annual_inc),2),round(avg(loan_amnt),2)
from loan 
group by home_ownership 
order by round(avg(annual_inc),2);
```
![loan8](/Users/hui2046/Desktop/loan8.png)

notes: 贷款客户中近半数是贷款买房（49.16%），平均年收入最高（88350美元)，平均贷款金额最高（16693美元)；租房客户占比（39.58%），平均年收入在66631美元以上；自有房屋占比11.19%，平均年收入72717美元。

## 贷款目的，贷款金额和年收入分析

```mysql
select purpose, count(purpose),round(avg(loan_amnt),2),round(avg(annual_inc),2)
from loan 
group by purpose 
order by count(purpose) desc;
```
![loan11](/Users/hui2046/Desktop/loan11.png)
notes: 贷款目的为债务合并的最多（56.52%），其次是还信用卡（22.86%）,用于家庭生活改善的占比6.65%。

## 贷款客户居住州，贷款金额和年收入分析

```mysql
select addr_state, count(addr_state),round(avg(loan_amnt),2),round(avg(annual_inc),2)
from loan 
group by addr_state
order by count(addr_state) desc;
```
![loan12](/Users/hui2046/Desktop/loan12.png)
notes: 贷款客户的地域分布上，加利福尼亚州最多（13.91%), 其次是纽约州（8.24%）和德克萨斯州（8.24%）。

## 贷款状态，贷款总额和客户年收入分析

```mysql
select loan_status,count(loan_status),round(sum(loan_amnt),2),round(avg(annual_inc),2)
from loan
group by loan_status
order by round(sum(loan_amnt),2) desc;
```
![loan9](/Users/hui2046/Desktop/loan9.png)

notes: 贷款已还清的客户占比46.09%，贷款正在进行中的占比40.68%，贷款违约率0.00137%。