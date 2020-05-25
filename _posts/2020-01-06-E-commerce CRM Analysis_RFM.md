# E-commerce CRM analysis case 
# RFM客户分层模型：精细化运营分析
## 问题：电商公司客户粘度如何？如何精细化客户群体及进一步营销管理？
## 该数据共包含28833条记录，9个字段

# Import data


```python
import pandas as pd 
import numpy as np
import os 
```


```python
os.chdir('/Users/hui2046/Downloads/SQL+Python/RFM数据')
df = pd.read_excel('电商用户RFM分析.xlsx')
```

# 数据概览


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 28833 entries, 0 to 28832
    Data columns (total 9 columns):
    品牌名称    28833 non-null object
    买家昵称    28833 non-null object
    付款日期    28833 non-null datetime64[ns]
    订单状态    28833 non-null object
    实付金额    28833 non-null int64
    邮费      28833 non-null int64
    省份      28833 non-null object
    城市      28832 non-null object
    购买数量    28833 non-null int64
    dtypes: datetime64[ns](1), int64(3), object(5)
    memory usage: 2.0+ MB



```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>品牌名称</th>
      <th>买家昵称</th>
      <th>付款日期</th>
      <th>订单状态</th>
      <th>实付金额</th>
      <th>邮费</th>
      <th>省份</th>
      <th>城市</th>
      <th>购买数量</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>JOJO</td>
      <td>叫我李2</td>
      <td>2019-01-01 00:17:59</td>
      <td>交易成功</td>
      <td>186</td>
      <td>6</td>
      <td>上海</td>
      <td>上海市</td>
      <td>1</td>
    </tr>
    <tr>
      <td>1</td>
      <td>JOJO</td>
      <td>0cyb1992</td>
      <td>2019-01-01 00:59:54</td>
      <td>交易成功</td>
      <td>145</td>
      <td>0</td>
      <td>广东省</td>
      <td>广州市</td>
      <td>1</td>
    </tr>
    <tr>
      <td>2</td>
      <td>JOJO</td>
      <td>萝污萌莉</td>
      <td>2019-01-01 07:48:48</td>
      <td>交易成功</td>
      <td>194</td>
      <td>8</td>
      <td>山东省</td>
      <td>东营市</td>
      <td>1</td>
    </tr>
    <tr>
      <td>3</td>
      <td>JOJO</td>
      <td>atblovemyy</td>
      <td>2019-01-01 09:15:49</td>
      <td>付款以后用户退款成功，交易自动关闭</td>
      <td>84</td>
      <td>0</td>
      <td>江苏省</td>
      <td>镇江市</td>
      <td>1</td>
    </tr>
    <tr>
      <td>4</td>
      <td>JOJO</td>
      <td>小星期鱼</td>
      <td>2019-01-01 09:59:33</td>
      <td>付款以后用户退款成功，交易自动关闭</td>
      <td>74</td>
      <td>0</td>
      <td>上海</td>
      <td>上海市</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 查看多少种订单状态，[].unique()

df['订单状态'].unique()
```




    array(['交易成功', '付款以后用户退款成功，交易自动关闭'], dtype=object)



# 数据清洗


```python
# 选取订单状态为‘交易成功’的记录

df = df.loc[df['订单状态'] == '交易成功',:]
```


```python
# 选取需要的关键字段作表格[['']],RFM:用户名，付款日期，支付金额

df = df[['买家昵称','付款日期','实付金额']]
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>买家昵称</th>
      <th>付款日期</th>
      <th>实付金额</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>叫我李2</td>
      <td>2019-01-01 00:17:59</td>
      <td>186</td>
    </tr>
    <tr>
      <td>1</td>
      <td>0cyb1992</td>
      <td>2019-01-01 00:59:54</td>
      <td>145</td>
    </tr>
    <tr>
      <td>2</td>
      <td>萝污萌莉</td>
      <td>2019-01-01 07:48:48</td>
      <td>194</td>
    </tr>
    <tr>
      <td>5</td>
      <td>重碎叠</td>
      <td>2019-01-01 10:00:07</td>
      <td>197</td>
    </tr>
    <tr>
      <td>6</td>
      <td>iho_jann</td>
      <td>2019-01-01 10:00:08</td>
      <td>168</td>
    </tr>
  </tbody>
</table>
</div>



# RFM模型建立

## R值：计算最近未消费日天数


```python
# 选取出最近的交易日期

r = df.groupby('买家昵称')['付款日期'].max().reset_index()
r.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>买家昵称</th>
      <th>付款日期</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>2019-02-04 17:49:34.000</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>2019-01-29 14:17:15.000</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>2019-01-11 03:46:18.000</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>2019-01-11 02:26:33.000</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>2019-06-28 16:53:26.458</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 计算未消费的天数 to_datetime, dt.days

r['R'] = (pd.to_datetime('2019-7-1') - r['付款日期']).dt.days
```


```python
# 选取需要的字段建表格[['']]

r = r[['买家昵称','R']]
r.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>买家昵称</th>
      <th>R</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>146</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>152</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>170</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>170</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



## F值：计算消费频率


```python
# 引入’日期标签‘字符串列，用于稍后合并’一天内多次购买‘为一次

df['日期标签'] = df['付款日期'].astype(str)

# 按'买家昵称','日期标签'分组计算消费频率（按天）
dup_f = df.groupby(['买家昵称','日期标签'])['付款日期'].count().reset_index()
dup_f.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>买家昵称</th>
      <th>日期标签</th>
      <th>付款日期</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>2019-02-04 17:49:34.000</td>
      <td>1</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>2019-01-29 14:17:15.000</td>
      <td>1</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>2019-01-11 03:46:18.000</td>
      <td>1</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>2019-01-11 02:26:33.000</td>
      <td>1</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>2019-06-28 16:53:26.458</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 新建f = ,按'买家昵称'分组，按付款日期聚合

f = dup_f.groupby('买家昵称')['付款日期'].count().reset_index()
f.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>买家昵称</th>
      <th>付款日期</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>1</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>1</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>1</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>1</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 将‘付款日期’替换为消费频率‘F‘

f.columns = ['买家昵称','F']
f.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>买家昵称</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>1</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>1</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>1</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>1</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



## M值：计算消费金额/次


```python
# 计算每个买家总消费金额:['实付金额'].sum()

sum_m = df.groupby('买家昵称')['实付金额'].sum().reset_index()

# 将['实付金额'].sum()列更名为['总支付金额']
sum_m.columns = ['买家昵称','总支付金额']
sum_m.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>买家昵称</th>
      <th>总支付金额</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>49</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>183</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>34</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>37</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>164</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 合并表：sum_m和f
com_m = pd.merge(sum_m,f,on = '买家昵称',how = 'inner')

#计算用户平均支付金额,并定义为 ’M‘
com_m['M'] = com_m['总支付金额'] / com_m['F']
com_m.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>买家昵称</th>
      <th>总支付金额</th>
      <th>F</th>
      <th>M</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>49</td>
      <td>1</td>
      <td>49.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>183</td>
      <td>1</td>
      <td>183.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>34</td>
      <td>1</td>
      <td>34.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>37</td>
      <td>1</td>
      <td>37.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>164</td>
      <td>1</td>
      <td>164.0</td>
    </tr>
  </tbody>
</table>
</div>



## 三表合并，建立RFM表


```python
rfm = pd.merge(r,com_m, on = '买家昵称', how= 'inner')
```


```python
# 选择需要的列
rfm = rfm[['买家昵称','R','F','M']]
```


```python
rfm.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>买家昵称</th>
      <th>R</th>
      <th>F</th>
      <th>M</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>146</td>
      <td>1</td>
      <td>49.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>152</td>
      <td>1</td>
      <td>183.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>170</td>
      <td>1</td>
      <td>34.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>170</td>
      <td>1</td>
      <td>37.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>2</td>
      <td>1</td>
      <td>164.0</td>
    </tr>
  </tbody>
</table>
</div>



# 打分框架确定


```python
# R值根据行业经验，设置为30天一个跨度，区间左闭右开：
# 1分-[120天,..); 2-[90,120);3-[60,90);4-[30,60);5-[0,30)
```


```python
# F值和购买频次挂钩，每多一次购买，分值就多加一分
# 1分-1次; 2分-2次;3分-3次;4分-4次;5分-[5,...)
```


```python
# M值做简单的区间统计，然后分组，这里我们按照50元的一个区间来进行划分：
# 1分-[0,50);2-[50,100);3-[100,150);4-[150,200);5-[200,250)
```

# 分值计算


```python
# 区间计算分值：cut(要切分的数据列,bins-按照什么区间进行分组,labels,right-右侧区间是开还是闭)
# right如果设置成False，就代表[0,30)，包含左侧的分组数据而不含右侧，若设置为True，则是[0,30]，首尾都包含。
# pd.cut().astype(float),转为浮点数

rfm['R-Score'] = pd.cut(rfm['R'],bins=[0,30,60,90,120,10000000],labels=[5,4,3,2,1],
                        right = False).astype(float)
rfm.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>买家昵称</th>
      <th>R</th>
      <th>F</th>
      <th>M</th>
      <th>R-Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>146</td>
      <td>1</td>
      <td>49.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>152</td>
      <td>1</td>
      <td>183.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>170</td>
      <td>1</td>
      <td>34.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>170</td>
      <td>1</td>
      <td>37.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>2</td>
      <td>1</td>
      <td>164.0</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
rfm['F-SCORE'] = pd.cut(rfm['F'],bins = [1,2,3,4,5,1000000],labels = [1,2,3,4,5],
                        right = False).astype(float)
rfm['M-SCORE'] = pd.cut(rfm['M'],bins = [0,50,100,150,200,1000000],labels = [1,2,3,4,5],
                        right = False).astype(float)
rfm.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>买家昵称</th>
      <th>R</th>
      <th>F</th>
      <th>M</th>
      <th>R-Score</th>
      <th>F-SCORE</th>
      <th>M-SCORE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>146</td>
      <td>1</td>
      <td>49.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>152</td>
      <td>1</td>
      <td>183.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>170</td>
      <td>1</td>
      <td>34.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>170</td>
      <td>1</td>
      <td>37.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>2</td>
      <td>1</td>
      <td>164.0</td>
      <td>5.0</td>
      <td>1.0</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>



# 客户分层

## RFM各值与平均值比较


```python
# 增加各分数与平均值对比列，减少客户分类数量

rfm['R是否大于均值'] = (rfm['R-Score'] > rfm['R-Score'].mean()) * 1
rfm['F是否大于均值'] = (rfm['F-SCORE'] > rfm['F-SCORE'].mean()) * 1
rfm['M是否大于均值'] = (rfm['M-SCORE'] > rfm['M-SCORE'].mean()) * 1
rfm.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>买家昵称</th>
      <th>R</th>
      <th>F</th>
      <th>M</th>
      <th>R-Score</th>
      <th>F-SCORE</th>
      <th>M-SCORE</th>
      <th>R是否大于均值</th>
      <th>F是否大于均值</th>
      <th>M是否大于均值</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>146</td>
      <td>1</td>
      <td>49.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>152</td>
      <td>1</td>
      <td>183.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>4.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>170</td>
      <td>1</td>
      <td>34.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>170</td>
      <td>1</td>
      <td>37.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>2</td>
      <td>1</td>
      <td>164.0</td>
      <td>5.0</td>
      <td>1.0</td>
      <td>4.0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



## RFM综合得分


```python
# 为客户分类引入RFM综合评分项

rfm['RFM分数'] = (rfm['R是否大于均值'] * 100) + (rfm['F是否大于均值'] * 10) + (rfm['M是否大于均值'] * 1)
rfm.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>买家昵称</th>
      <th>R</th>
      <th>F</th>
      <th>M</th>
      <th>R-Score</th>
      <th>F-SCORE</th>
      <th>M-SCORE</th>
      <th>R是否大于均值</th>
      <th>F是否大于均值</th>
      <th>M是否大于均值</th>
      <th>RFM分数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>146</td>
      <td>1</td>
      <td>49.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>152</td>
      <td>1</td>
      <td>183.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>4.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>170</td>
      <td>1</td>
      <td>34.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>170</td>
      <td>1</td>
      <td>37.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>2</td>
      <td>1</td>
      <td>164.0</td>
      <td>5.0</td>
      <td>1.0</td>
      <td>4.0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>101</td>
    </tr>
  </tbody>
</table>
</div>



## 基于RFM得分，对客群分类贴标


```python
#判断R/F/M是否大于均值
def transform_label(x):
    if x == 111:
        label = '重要价值客户'
    elif x == 110:
        label = '消费潜力客户'
    elif x == 101:
        label = '频次深耕客户'
    elif x == 100:
        label = '新客户'
    elif x == 11:
        label = '重要价值流失预警客户'
    elif x == 10:
        label = '一般客户'
    elif x == 1:
        label = '高消费唤回客户'
    elif x == 0:
        label = '流失客户'
    return label

```


```python
# 贴标函数运用 apply.

rfm['人群类型'] = rfm['RFM分数'].apply(transform_label)
rfm.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>买家昵称</th>
      <th>R</th>
      <th>F</th>
      <th>M</th>
      <th>R-Score</th>
      <th>F-SCORE</th>
      <th>M-SCORE</th>
      <th>R是否大于均值</th>
      <th>F是否大于均值</th>
      <th>M是否大于均值</th>
      <th>RFM分数</th>
      <th>人群类型</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>146</td>
      <td>1</td>
      <td>49.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>流失客户</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>152</td>
      <td>1</td>
      <td>183.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>4.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>高消费唤回客户</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>170</td>
      <td>1</td>
      <td>34.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>流失客户</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>170</td>
      <td>1</td>
      <td>37.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>流失客户</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>2</td>
      <td>1</td>
      <td>164.0</td>
      <td>5.0</td>
      <td>1.0</td>
      <td>4.0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>101</td>
      <td>频次深耕客户</td>
    </tr>
  </tbody>
</table>
</div>



## 统计客群人数和金额


```python
# 人数统计

count = rfm['人群类型'].value_counts().reset_index()
count.columns = ['客户类型','人数']
count['人数占比'] = count['人数'] / count['人数'].sum()
count
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>客户类型</th>
      <th>人数</th>
      <th>人数占比</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>高消费唤回客户</td>
      <td>7155</td>
      <td>0.281471</td>
    </tr>
    <tr>
      <td>1</td>
      <td>流失客户</td>
      <td>6671</td>
      <td>0.262431</td>
    </tr>
    <tr>
      <td>2</td>
      <td>频次深耕客户</td>
      <td>5350</td>
      <td>0.210464</td>
    </tr>
    <tr>
      <td>3</td>
      <td>新客户</td>
      <td>4218</td>
      <td>0.165932</td>
    </tr>
    <tr>
      <td>4</td>
      <td>重要价值客户</td>
      <td>811</td>
      <td>0.031904</td>
    </tr>
    <tr>
      <td>5</td>
      <td>重要价值流失预警客户</td>
      <td>486</td>
      <td>0.019119</td>
    </tr>
    <tr>
      <td>6</td>
      <td>消费潜力客户</td>
      <td>478</td>
      <td>0.018804</td>
    </tr>
    <tr>
      <td>7</td>
      <td>一般客户</td>
      <td>251</td>
      <td>0.009874</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 消费金额统计

rfm['购买总金额'] = rfm['F'] * rfm['M']
mon = rfm.groupby('人群类型')['购买总金额'].sum().reset_index()
mon.columns = ['客户类型','消费金额']
mon['金额占比'] = mon['消费金额'] / mon['消费金额'].sum()
mon
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>客户类型</th>
      <th>消费金额</th>
      <th>金额占比</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>一般客户</td>
      <td>35948.0</td>
      <td>0.010238</td>
    </tr>
    <tr>
      <td>1</td>
      <td>新客户</td>
      <td>270412.0</td>
      <td>0.077012</td>
    </tr>
    <tr>
      <td>2</td>
      <td>流失客户</td>
      <td>443863.0</td>
      <td>0.126410</td>
    </tr>
    <tr>
      <td>3</td>
      <td>消费潜力客户</td>
      <td>68422.0</td>
      <td>0.019486</td>
    </tr>
    <tr>
      <td>4</td>
      <td>重要价值客户</td>
      <td>286705.0</td>
      <td>0.081652</td>
    </tr>
    <tr>
      <td>5</td>
      <td>重要价值流失预警客户</td>
      <td>156674.0</td>
      <td>0.044620</td>
    </tr>
    <tr>
      <td>6</td>
      <td>频次深耕客户</td>
      <td>960528.0</td>
      <td>0.273553</td>
    </tr>
    <tr>
      <td>7</td>
      <td>高消费唤回客户</td>
      <td>1288753.0</td>
      <td>0.367030</td>
    </tr>
  </tbody>
</table>
</div>




```python
result = pd.merge(count,mon, on = '客户类型')
result
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>客户类型</th>
      <th>人数</th>
      <th>人数占比</th>
      <th>消费金额</th>
      <th>金额占比</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>高消费唤回客户</td>
      <td>7155</td>
      <td>0.281471</td>
      <td>1288753.0</td>
      <td>0.367030</td>
    </tr>
    <tr>
      <td>1</td>
      <td>流失客户</td>
      <td>6671</td>
      <td>0.262431</td>
      <td>443863.0</td>
      <td>0.126410</td>
    </tr>
    <tr>
      <td>2</td>
      <td>频次深耕客户</td>
      <td>5350</td>
      <td>0.210464</td>
      <td>960528.0</td>
      <td>0.273553</td>
    </tr>
    <tr>
      <td>3</td>
      <td>新客户</td>
      <td>4218</td>
      <td>0.165932</td>
      <td>270412.0</td>
      <td>0.077012</td>
    </tr>
    <tr>
      <td>4</td>
      <td>重要价值客户</td>
      <td>811</td>
      <td>0.031904</td>
      <td>286705.0</td>
      <td>0.081652</td>
    </tr>
    <tr>
      <td>5</td>
      <td>重要价值流失预警客户</td>
      <td>486</td>
      <td>0.019119</td>
      <td>156674.0</td>
      <td>0.044620</td>
    </tr>
    <tr>
      <td>6</td>
      <td>消费潜力客户</td>
      <td>478</td>
      <td>0.018804</td>
      <td>68422.0</td>
      <td>0.019486</td>
    </tr>
    <tr>
      <td>7</td>
      <td>一般客户</td>
      <td>251</td>
      <td>0.009874</td>
      <td>35948.0</td>
      <td>0.010238</td>
    </tr>
  </tbody>
</table>
</div>



# 模型代码写入函数


```python
#输入数据文件名
def get_rfm(name = '电商用户RFM分析.xlsx'):
    df = pd.read_excel(name)
    df = df.loc[df['订单状态'] == '交易成功',:]
   
    df = df[['买家昵称','付款日期','实付金额']]

    r = df.groupby('买家昵称')['付款日期'].max().reset_index()
    r['R'] = (pd.to_datetime('2019-7-1') - r['付款日期']).dt.days
    r = r[['买家昵称','R']]

    #引入日期标签列
    df['日期标签'] = df['付款日期'].astype(str)

    #单个用户一天内订单合并
    dup_f = df.groupby(['买家昵称','日期标签'])['付款日期'].count().reset_index()

    #对合并后的用户统计频次
    f = dup_f.groupby('买家昵称')['付款日期'].count().reset_index()
    f.columns = ['买家昵称','F']

    sum_m = df.groupby('买家昵称')['实付金额'].sum().reset_index()
    sum_m.columns = ['买家昵称','总支付金额']
    com_m = pd.merge(sum_m,f,left_on = '买家昵称',right_on = '买家昵称',how = 'inner')

    #计算用户平均支付金额
    com_m['M'] = com_m['总支付金额'] / com_m['F']

    rfm = pd.merge(r,com_m,left_on = '买家昵称',right_on = '买家昵称',how = 'inner')
    rfm = rfm[['买家昵称','R','F','M']]


    rfm['R-SCORE'] = pd.cut(rfm['R'],bins = [0,30,60,90,120,1000000],labels = [5,4,3,2,1],right = False).astype(float)
    rfm['F-SCORE'] = pd.cut(rfm['F'],bins = [1,2,3,4,5,1000000],labels = [1,2,3,4,5],right = False).astype(float)
    rfm['M-SCORE'] = pd.cut(rfm['M'],bins = [0,50,100,150,200,1000000],labels = [1,2,3,4,5],right = False).astype(float)

    rfm['R是否大于均值'] = (rfm['R-SCORE'] > rfm['R-SCORE'].mean()) * 1
    rfm['F是否大于均值'] = (rfm['F-SCORE'] > rfm['F-SCORE'].mean()) * 1
    rfm['M是否大于均值'] = (rfm['M-SCORE'] > rfm['M-SCORE'].mean()) * 1

    rfm['RMF分数'] = (rfm['R是否大于均值'] * 100) + (rfm['F是否大于均值'] * 10) + (rfm['M是否大于均值'] * 1)

    rfm['人群类型'] = rfm['RMF分数'].apply(transform_label)

    count = rfm['人群类型'].value_counts().reset_index()
    count.columns = ['客户类型','人数']
    count['人数占比'] = count['人数'] / count['人数'].sum()

    rfm['购买总金额'] = rfm['F'] * rfm['M']
    mon = rfm.groupby('人群类型')['购买总金额'].sum().reset_index()
    mon.columns = ['客户类型','消费金额']
    mon['金额占比'] = mon['消费金额'] / mon['消费金额'].sum()

    result = pd.merge(count,mon,left_on = '客户类型',right_on = '客户类型')

    return result


#判断R/F/M是否大于均值
def transform_label(x):
    if x == 111:
        label = '重要价值客户'
    elif x == 110:
        label = '消费潜力客户'
    elif x == 101:
        label = '频次深耕客户'
    elif x == 100:
        label = '新客户'
    elif x == 11:
        label = '重要价值流失预警客户'
    elif x == 10:
        label = '一般客户'
    elif x == 1:
        label = '高消费唤回客户'
    elif x == 0:
        label = '流失客户'
    return label
```


```python
re_rfm = get_rfm(name = '电商用户RFM分析.xlsx')
re_rfm
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>客户类型</th>
      <th>人数</th>
      <th>人数占比</th>
      <th>消费金额</th>
      <th>金额占比</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>高消费唤回客户</td>
      <td>7155</td>
      <td>0.281471</td>
      <td>1288753.0</td>
      <td>0.367030</td>
    </tr>
    <tr>
      <td>1</td>
      <td>流失客户</td>
      <td>6671</td>
      <td>0.262431</td>
      <td>443863.0</td>
      <td>0.126410</td>
    </tr>
    <tr>
      <td>2</td>
      <td>频次深耕客户</td>
      <td>5350</td>
      <td>0.210464</td>
      <td>960528.0</td>
      <td>0.273553</td>
    </tr>
    <tr>
      <td>3</td>
      <td>新客户</td>
      <td>4218</td>
      <td>0.165932</td>
      <td>270412.0</td>
      <td>0.077012</td>
    </tr>
    <tr>
      <td>4</td>
      <td>重要价值客户</td>
      <td>811</td>
      <td>0.031904</td>
      <td>286705.0</td>
      <td>0.081652</td>
    </tr>
    <tr>
      <td>5</td>
      <td>重要价值流失预警客户</td>
      <td>486</td>
      <td>0.019119</td>
      <td>156674.0</td>
      <td>0.044620</td>
    </tr>
    <tr>
      <td>6</td>
      <td>消费潜力客户</td>
      <td>478</td>
      <td>0.018804</td>
      <td>68422.0</td>
      <td>0.019486</td>
    </tr>
    <tr>
      <td>7</td>
      <td>一般客户</td>
      <td>251</td>
      <td>0.009874</td>
      <td>35948.0</td>
      <td>0.010238</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
