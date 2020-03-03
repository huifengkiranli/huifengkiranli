# MySQL: UK E-Commerce data modeling
# 1. 这是一个跨国数据集，包含2010年12月1日至2011年12月9日之间在英国注册的非商店在线零售的所有交易。该公司主要销售各种独特的礼品，许多客户是该公司批发商.
# 2. Operations management issues: 该公司客户主要集中在哪些国家？如何精细化客户群体及进一步营销管理？ 
# 3. Data information: 该数据集时间跨度为2010年12月1日至2011年12月9日，共包含541909条记录，8个字段： CustomerID, InvoiceNo, InvoiceDate, Quantity, UnitPrice, Country，Description, StockCode
# 4. Data Preparation
### - 基于RFM模型需要，新建一个表data1，在该表中将去掉两个字段：StockCode和Description, MySQL code 如下：

``` mysql
create table data1 
as select CustomerID,InvoiceNo,InvoiceDate,Quantity,UnitPrice,Country from UK_data
select * from data1
```
![UK1](images/UK1.png)
## -1. 处理缺失值null, case when then else end：
``` mysql
select sum(case when CustomerID is null then 1 else 0 end) as 'sum_customerid',
       sum(case when InvoiceNo  is null then 1 else 0 end) as 'sum_invocieNo',
       sum(case when InvoiceDate is null then 1 else 0 end) as 'sum_invoiceDate',
       sum(case when Quantity    is null then 1 else 0 end) as 'sum_quantity',
       sum(case when UnitPrice   is null then 1 else 0 end) as 'sun_unitprice',
       sum(case when Country     is null then 1 else 0 end)as 'sum_country'
from data1;
```
* 注意点：MySQL does not accept spaces between function name and parenthesis, unless you have set SQL_MODE=IGNORE_SPACE but that gives you other undesirable side effects, eg. **sum_()**.

![UK2](images/UK2.png)

查询结果可知，customerid存有135080个null，缺失率占比24.9%，数据丢失比较严重，需询问相关负责人查找原因，因无法知晓原因，将缺失值全部换成0处理，并把结果重新创建一个表data2, code 如下：

``` mysql
create table data2 
select coalesce(CustomerID,0)as CustomerID,InvoiceNo,InvoiceDate,Quantity,UnitPrice,Country 
from data1;
```
* 注意点：将null值的字段转为0：coalesce(customerid,0)

第一步的CustomerID中的缺失值处理完毕。

##  - 2.处理异常值
首先，查看InvoiceDate、Quantity、UnitPrice是否存在异常值，**max()&min()**

``` mysql
select max(InvoiceDate),min(InvoiceDate), max(Quantity),min(Quantity),
max(UnitPrice),min(UnitPrice)
from data2;
```
![UK3](images/UK3.png)

结果显示：日期不存在异常值，Quantity、UnitPrice均存在异常值.

### 1. 处理Quantity中的异常值
```mysql
select * from data2 where Quantity <=0;
```

![UK4](images/UK4.png)

可见Quantity中的异常值，共10624个，共同特征：InvoiceNo.皆以C开头，按实际分析，应该为退货处理，需要重点分析是什么原因造成的退货？本次练习主要是建立RFM模型，不分析退货原因，所以需把这些异常值删除 **delete from...where..**，实现代码如下:

```mysql
delete from data2 where Quantity <=0;
```

### 2. 处理UnitPrice的异常值

```mysql
select * from data2 where UnitPrice <=0;
```

![UK5](images/UK5.png)

查询可知:1181条记录单价大多数为零，实际分析应该为赠品，对于单价为负值的，应为公司损失的商品，所以这两种应删除, **delete from ...where...**

```mysql
delete from data2 where UnitPrice <=0;
```

##  - 3. 数据格式一致化处理
### 1. 日期格式：数据集中InvoiceDate的日期不利于查询，处理代码如下：
```mysql
alter table data2 add column InvoiceDatetime varchar(255) not NULL
update data2 set InvoiceDatetime = STR_TO_DATE(InvoiceDate,'%m/%d/%Y %H:%i')；
```

删除原来的列InvoiceDate

```mysql
alter table data2 drop InvoiceDate;
```

![UK6](images/UK6.png)

日期处理：(**str_to_date()**)

### 2. RFM模型，还需要增加Monetary列

```mysql
alter table data2 add column Monetary float not NULL
update data2 set Monetary = Quantity*UnitPrice;
```

![UK7](images/UK7.png)

## - 4. 重复值处理
新建表data3用以insert distinct * from data2, code as belows:

``` mysql
create table data3 like data2
insert into data3 select distinct* from data2 
select * from data3;
```

![UK8](images/UK8.png)

数据已全部清洗完毕，由图可知，CustomerID、InvoiceNo中仍然有重复值，从实际经验分析，CustomerID有重复值，说明客户有重复购买行为，而InvoiceNo中有重复值说明客户一次购买了多种商品，因本文研究的是FRM模型，即可以把每一个不同的InvoiceNo代表一次购买行为发生。

Notes:  **create table like /as comparison**:

* 半自动化模式create table like.....其创建的表除了表名和源表不一样外，其余所有的细节都是一样的。但是没有源表的数据。所以这种create  table like的形式非常适合对源表模式的复制。
* 懒人模式 create table as select...创建的表，非分区表,不管源表是否是分区表，一定要注意分区功能的丢失。当然创建表以后可以添加分区，成为分区表。如果select选择的是指定的列则不会有这种问题。
* 使用CTAS方式创建的表不能是外部表。

# 5. Data Modeling-RFM
## 1. RFM模型是衡量客户价值和利润贡献能力的重要工具，通过研究客户最近期的购买行为、购买频率以及购买金额来判定客户价值，从而实现对客户精细化地分层，为客户关系管理或者客户营销运营管理提供数据支持。

|     Letter | Description |
| ----------- | ----------- |
| R    | 最近的一次购买时间点      |
| F   | 消费频率，下订单总量       |
| M   | 消费总金额      |

因此需要求出与上述三个相关的衡量指标：即(至数据截止日）天数差R、消费频率F、消费金额M并合并数据创建新表RFM， 代码如下:

```mysql
create table RFM 
as select CustomerID, InvoiceNo,Quantity,UnitPrice,Country,InvoiceDatetime,
datediff('2011-12-09',MAX(InvoiceDatetime)) as 'R',
count(InvoiceNo) as 'F',
round(SUM(Monetary),2) as 'M'
FROM data3
group by CustomerID, InvoiceNo,Quantity,UnitPrice,Country,InvoiceDatetime
order by R desc, F desc, M desc;
```
* 注意：group by 后面的字段必须和前面的select后面的字段一样，且最好不用select*
* 求天数差： **datediff(' ', max())**
* 金额总和四舍五入保留小数点后两位：**round(sum(' '),2)**
* 多注意标点符号错误，especially comma

![UK9](images/UK9.png)

## 2. create RFMscore table
RFM中三项R,F,M 的评分标准是需要根据行业特点和公司发展战略来定的，每个区间如何定，可以多参考行业报告，对比分析后来确定，因为本文行业是电商行业，所以本文评分标准确定如下：

|     R | Rscore |        
| ----- | ----- |
|  <= 30  | 5      |
| (30,90]  | 4      |
| (90,180]   | 3     |
|  (180,365]  | 2     |
| > 365 | 1    |

|     F | Fscore |
| ----- | ----- |
|  > 80  | 5      |
| (20,80]  | 4      |
| (10,20]   | 3     |
|  (5,10]  | 2     |
| <= 5 | 1    |

|     M | Mscore |
| ----- | ----- |
|  > 10000  | 5      |
| (5000,10000]  | 4      |
| (1000,5000]   | 3     |
|  (300,1000]  | 2     |
| <= 300 | 1    |

实现代码如下：

```mysql
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
```
![UK10](images/UK10.png)

* 注意 select* 后面的comma别忘记

## 3. create RFMvalue table
### -1. 首先，根据K-means原理，计算R,F,M的三项的算数平均值Avg，了解分区间后RFMscore与平均值相比，处于怎样的位置，代码如下：
```mysql
select ROUND(AVG(Rscore),1) as Ravg,
         ROUND(AVG(Fscore),1) as Favg,
         ROUND(AVG(Mscore),1) as Mavg from RFMscore;
```
![UK11](images/UK11.png)

### -2. create RFMvalue table: 将RFMscore得分 vs. RFMavg平均值，对比后给RFMscore赋予1或0的value，代码如下：
```mysql
create table RFMvalue as select *,
(case when Rscore > 3.1 then 1 else 0 end) as Rvalue,
(case when Fscore > 1 then 1 else 0 end) as Fvalue,
(case when Mscore > 1 then 1 else 0 end) as Mvalue from RFMscore;
```

![UK12](images/UK12.png)

### -3. segment customers： 根据RFM模型理论将客户分层
![UK13](images/UK13.png)

根据RFM（图片来源：point小数点）理论，上升箭头表示大于均值，向下箭头表示小于均值。
写入中文字段前，修改编码：
```mysql
alter table RFMvalue convert to character set utf8;
```
客户分层实现代码如下：

```mysql
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

![UK14](images/UK14.png)

下个篇章将做数据可视化的练习。
