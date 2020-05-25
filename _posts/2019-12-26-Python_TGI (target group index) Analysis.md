# Python_TGI (target group index) Analysis
# TGI指标：Python分析电商客群特征

# 电商全国销售数据，对比分析各省市销售额

# 数据概览


```python
import pandas as pd 
import numpy as np
import os 
```


```python
os.chdir('/Users/hui2046/Downloads/SQL+Python/TGI指数_淘宝用户群分析')
df = pd.read_excel('TGI数据.xlsx')
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
      <td>viva la vida</td>
      <td>做快淘饭</td>
      <td>2019-04-18 00:03:00</td>
      <td>交易成功</td>
      <td>22.32</td>
      <td>0</td>
      <td>北京</td>
      <td>北京市</td>
      <td>1</td>
    </tr>
    <tr>
      <td>1</td>
      <td>viva la vida</td>
      <td>作自有世祟</td>
      <td>2019-02-17 00:03:51</td>
      <td>交易成功</td>
      <td>87.00</td>
      <td>0</td>
      <td>上海</td>
      <td>上海市</td>
      <td>1</td>
    </tr>
    <tr>
      <td>2</td>
      <td>viva la vida</td>
      <td>作雪白室</td>
      <td>2019-04-18 00:01:43</td>
      <td>交易成功</td>
      <td>97.66</td>
      <td>0</td>
      <td>福建省</td>
      <td>福州市</td>
      <td>2</td>
    </tr>
    <tr>
      <td>3</td>
      <td>viva la vida</td>
      <td>作美女购物主</td>
      <td>2019-01-11 23:35:01</td>
      <td>交易成功</td>
      <td>37.23</td>
      <td>0</td>
      <td>河南省</td>
      <td>安阳市</td>
      <td>3</td>
    </tr>
    <tr>
      <td>4</td>
      <td>viva la vida</td>
      <td>作美女购物主</td>
      <td>2019-02-18 14:16:03</td>
      <td>交易成功</td>
      <td>29.50</td>
      <td>0</td>
      <td>河南省</td>
      <td>安阳市</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 28832 entries, 0 to 28831
    Data columns (total 9 columns):
    品牌名称    28832 non-null object
    买家昵称    28832 non-null object
    付款日期    28832 non-null datetime64[ns]
    订单状态    28832 non-null object
    实付金额    28832 non-null float64
    邮费      28832 non-null int64
    省份      28832 non-null object
    城市      28832 non-null object
    购买数量    28832 non-null int64
    dtypes: datetime64[ns](1), float64(1), int64(2), object(5)
    memory usage: 2.0+ MB


# 分类客户并计算平均支付金额以贴标客户


```python
gp_user = df.groupby('买家昵称')['实付金额'].mean().reset_index()
gp_user.head()
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
      <th>实付金额</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>49.450</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>22.000</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>34.570</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>37.475</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>13.500</td>
    </tr>
  </tbody>
</table>
</div>




```python
def if_high(x):
    if x > 50:
        return '高客单'
    else:
        return '低客单'

gp_user['客单类别'] = gp_user['实付金额'].apply(if_high)
gp_user.head()
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
      <th>实付金额</th>
      <th>客单类别</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>49.450</td>
      <td>低客单</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>22.000</td>
      <td>低客单</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>34.570</td>
      <td>低客单</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>37.475</td>
      <td>低客单</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>13.500</td>
      <td>低客单</td>
    </tr>
  </tbody>
</table>
</div>



# 客单数据去重，和地域数据合并


```python
df_dup = df.loc[df.duplicated('买家昵称')== False,:]
```


```python
df_merge = pd.merge(gp_user,df_dup,left_on='买家昵称',right_on='买家昵称',
                   how ='inner')
df_merge.head()
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
      <th>实付金额_x</th>
      <th>客单类别</th>
      <th>品牌名称</th>
      <th>付款日期</th>
      <th>订单状态</th>
      <th>实付金额_y</th>
      <th>邮费</th>
      <th>省份</th>
      <th>城市</th>
      <th>购买数量</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>.blue_ram</td>
      <td>49.450</td>
      <td>低客单</td>
      <td>viva la vida</td>
      <td>2019-02-04 17:49:34.000</td>
      <td>交易成功</td>
      <td>49.450</td>
      <td>0</td>
      <td>上海</td>
      <td>上海市</td>
      <td>1</td>
    </tr>
    <tr>
      <td>1</td>
      <td>.christiny</td>
      <td>22.000</td>
      <td>低客单</td>
      <td>viva la vida</td>
      <td>2019-01-29 14:17:15.000</td>
      <td>交易成功</td>
      <td>22.000</td>
      <td>0</td>
      <td>江苏省</td>
      <td>南京市</td>
      <td>1</td>
    </tr>
    <tr>
      <td>2</td>
      <td>.willn1</td>
      <td>34.570</td>
      <td>低客单</td>
      <td>viva la vida</td>
      <td>2019-01-11 03:46:18.000</td>
      <td>交易成功</td>
      <td>34.570</td>
      <td>0</td>
      <td>山东省</td>
      <td>烟台市</td>
      <td>2</td>
    </tr>
    <tr>
      <td>3</td>
      <td>.托托m</td>
      <td>37.475</td>
      <td>低客单</td>
      <td>viva la vida</td>
      <td>2019-01-11 02:26:33.000</td>
      <td>交易成功</td>
      <td>37.475</td>
      <td>0</td>
      <td>上海</td>
      <td>上海市</td>
      <td>3</td>
    </tr>
    <tr>
      <td>4</td>
      <td>0000妮</td>
      <td>13.500</td>
      <td>低客单</td>
      <td>viva la vida</td>
      <td>2019-06-28 16:53:26.458</td>
      <td>交易成功</td>
      <td>13.500</td>
      <td>0</td>
      <td>广东省</td>
      <td>揭阳市</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



# 统计各省市高低客单人数pivot_table


```python
#先筛选出需要的列
df_merge = df_merge[['买家昵称','客单类别','省份','城市']]
```


```python
#pivot_table
result = pd.pivot_table(df_merge,index = ['省份','城市'],columns='客单类别',aggfunc='count')
result.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th colspan="2" halign="left">买家昵称</th>
    </tr>
    <tr>
      <th></th>
      <th>客单类别</th>
      <th>低客单</th>
      <th>高客单</th>
    </tr>
    <tr>
      <th>省份</th>
      <th>城市</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>上海</td>
      <td>上海市</td>
      <td>2818.0</td>
      <td>2374.0</td>
    </tr>
    <tr>
      <td rowspan="4" valign="top">云南省</td>
      <td>临沧市</td>
      <td>3.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>丽江市</td>
      <td>1.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>保山市</td>
      <td>6.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>大理白族自治州</td>
      <td>9.0</td>
      <td>8.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#高低客单数据合并
tgi = pd.merge(result['买家昵称']['高客单'].reset_index(),result['买家昵称']['低客单'].reset_index(),
               on=['省份','城市'],how='inner')
tgi.head()
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
      <th>省份</th>
      <th>城市</th>
      <th>高客单</th>
      <th>低客单</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>上海</td>
      <td>上海市</td>
      <td>2374.0</td>
      <td>2818.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>云南省</td>
      <td>临沧市</td>
      <td>2.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>云南省</td>
      <td>丽江市</td>
      <td>3.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>云南省</td>
      <td>保山市</td>
      <td>2.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>云南省</td>
      <td>大理白族自治州</td>
      <td>8.0</td>
      <td>9.0</td>
    </tr>
  </tbody>
</table>
</div>



# 计算各省市客单总数和高客单占比


```python
tgi['客单总数'] = tgi['高客单'] + tgi['低客单']
tgi['高客单占比'] = tgi['高客单']/ tgi['客单总数']

tgi.head()
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
      <th>省份</th>
      <th>城市</th>
      <th>高客单</th>
      <th>低客单</th>
      <th>高客单占比</th>
      <th>总人数</th>
      <th>客单总数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>上海</td>
      <td>上海市</td>
      <td>2374.0</td>
      <td>2818.0</td>
      <td>0.457242</td>
      <td>5192.0</td>
      <td>5192.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>云南省</td>
      <td>临沧市</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>0.400000</td>
      <td>5.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>云南省</td>
      <td>丽江市</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>0.750000</td>
      <td>4.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>云南省</td>
      <td>保山市</td>
      <td>2.0</td>
      <td>6.0</td>
      <td>0.250000</td>
      <td>8.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>云南省</td>
      <td>大理白族自治州</td>
      <td>8.0</td>
      <td>9.0</td>
      <td>0.470588</td>
      <td>17.0</td>
      <td>17.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 检查空值并删除
tgi.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 346 entries, 0 to 345
    Data columns (total 7 columns):
    省份       346 non-null object
    城市       346 non-null object
    高客单      332 non-null float64
    低客单      329 non-null float64
    高客单占比    315 non-null float64
    总人数      315 non-null float64
    客单总数     315 non-null float64
    dtypes: float64(5), object(2)
    memory usage: 31.6+ KB



```python
tgi.dropna()
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
      <th>省份</th>
      <th>城市</th>
      <th>高客单</th>
      <th>低客单</th>
      <th>高客单占比</th>
      <th>总人数</th>
      <th>客单总数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>上海</td>
      <td>上海市</td>
      <td>2374.0</td>
      <td>2818.0</td>
      <td>0.457242</td>
      <td>5192.0</td>
      <td>5192.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>云南省</td>
      <td>临沧市</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>0.400000</td>
      <td>5.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>云南省</td>
      <td>丽江市</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>0.750000</td>
      <td>4.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>云南省</td>
      <td>保山市</td>
      <td>2.0</td>
      <td>6.0</td>
      <td>0.250000</td>
      <td>8.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>云南省</td>
      <td>大理白族自治州</td>
      <td>8.0</td>
      <td>9.0</td>
      <td>0.470588</td>
      <td>17.0</td>
      <td>17.0</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>341</td>
      <td>黑龙江省</td>
      <td>绥化市</td>
      <td>2.0</td>
      <td>14.0</td>
      <td>0.125000</td>
      <td>16.0</td>
      <td>16.0</td>
    </tr>
    <tr>
      <td>342</td>
      <td>黑龙江省</td>
      <td>鸡西市</td>
      <td>3.0</td>
      <td>6.0</td>
      <td>0.333333</td>
      <td>9.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <td>343</td>
      <td>黑龙江省</td>
      <td>鹤岗市</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>0.666667</td>
      <td>3.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>344</td>
      <td>黑龙江省</td>
      <td>黑河市</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>0.428571</td>
      <td>7.0</td>
      <td>7.0</td>
    </tr>
    <tr>
      <td>345</td>
      <td>黑龙江省</td>
      <td>齐齐哈尔市</td>
      <td>10.0</td>
      <td>14.0</td>
      <td>0.416667</td>
      <td>24.0</td>
      <td>24.0</td>
    </tr>
  </tbody>
</table>
<p>315 rows × 7 columns</p>
</div>



# 计算高客单总占比


```python
total_percentage = tgi['高客单'].sum()/tgi['客单总数'].sum()
total_percentage
```




    0.4163255849872577



# 计算各城市高客单TGI指数


```python
tgi['高客单TGI'] = tgi['高客单占比']/total_percentage * 100
tgi = tgi.sort_values('高客单TGI',ascending = False)
tgi.head()
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
      <th>省份</th>
      <th>城市</th>
      <th>高客单</th>
      <th>低客单</th>
      <th>高客单占比</th>
      <th>总人数</th>
      <th>客单总数</th>
      <th>高客单TGI</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>149</td>
      <td>新疆维吾尔自治区</td>
      <td>哈密市</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>0.800000</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>192.157299</td>
    </tr>
    <tr>
      <td>152</td>
      <td>新疆维吾尔自治区</td>
      <td>巴音郭楞蒙古自治州</td>
      <td>10.0</td>
      <td>3.0</td>
      <td>0.769231</td>
      <td>13.0</td>
      <td>13.0</td>
      <td>184.766634</td>
    </tr>
    <tr>
      <td>2</td>
      <td>云南省</td>
      <td>丽江市</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>0.750000</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>180.147468</td>
    </tr>
    <tr>
      <td>277</td>
      <td>甘肃省</td>
      <td>白银市</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>0.750000</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>180.147468</td>
    </tr>
    <tr>
      <td>34</td>
      <td>吉林省</td>
      <td>辽源市</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>0.666667</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>160.131083</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 样本选择中，应选大于客单总数平均值
tgi.loc[tgi['客单总数'] > tgi['客单总数'].mean(),:].head(10)
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
      <th>省份</th>
      <th>城市</th>
      <th>高客单</th>
      <th>低客单</th>
      <th>高客单占比</th>
      <th>总人数</th>
      <th>客单总数</th>
      <th>高客单TGI</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>287</td>
      <td>福建省</td>
      <td>福州市</td>
      <td>145.0</td>
      <td>135.0</td>
      <td>0.517857</td>
      <td>280.0</td>
      <td>280.0</td>
      <td>124.387537</td>
    </tr>
    <tr>
      <td>124</td>
      <td>广东省</td>
      <td>珠海市</td>
      <td>49.0</td>
      <td>52.0</td>
      <td>0.485149</td>
      <td>101.0</td>
      <td>101.0</td>
      <td>116.531035</td>
    </tr>
    <tr>
      <td>27</td>
      <td>北京</td>
      <td>北京市</td>
      <td>1203.0</td>
      <td>1298.0</td>
      <td>0.481008</td>
      <td>2501.0</td>
      <td>2501.0</td>
      <td>115.536401</td>
    </tr>
    <tr>
      <td>283</td>
      <td>福建省</td>
      <td>厦门市</td>
      <td>105.0</td>
      <td>118.0</td>
      <td>0.470852</td>
      <td>223.0</td>
      <td>223.0</td>
      <td>113.097065</td>
    </tr>
    <tr>
      <td>111</td>
      <td>广东省</td>
      <td>佛山市</td>
      <td>118.0</td>
      <td>135.0</td>
      <td>0.466403</td>
      <td>253.0</td>
      <td>253.0</td>
      <td>112.028465</td>
    </tr>
    <tr>
      <td>173</td>
      <td>江西省</td>
      <td>南昌市</td>
      <td>63.0</td>
      <td>73.0</td>
      <td>0.463235</td>
      <td>136.0</td>
      <td>136.0</td>
      <td>111.267554</td>
    </tr>
    <tr>
      <td>46</td>
      <td>四川省</td>
      <td>成都市</td>
      <td>287.0</td>
      <td>334.0</td>
      <td>0.462158</td>
      <td>621.0</td>
      <td>621.0</td>
      <td>111.008746</td>
    </tr>
    <tr>
      <td>0</td>
      <td>上海</td>
      <td>上海市</td>
      <td>2374.0</td>
      <td>2818.0</td>
      <td>0.457242</td>
      <td>5192.0</td>
      <td>5192.0</td>
      <td>109.827963</td>
    </tr>
    <tr>
      <td>164</td>
      <td>江苏省</td>
      <td>无锡市</td>
      <td>135.0</td>
      <td>162.0</td>
      <td>0.454545</td>
      <td>297.0</td>
      <td>297.0</td>
      <td>109.180284</td>
    </tr>
    <tr>
      <td>120</td>
      <td>广东省</td>
      <td>深圳市</td>
      <td>438.0</td>
      <td>528.0</td>
      <td>0.453416</td>
      <td>966.0</td>
      <td>966.0</td>
      <td>108.909028</td>
    </tr>
  </tbody>
</table>
</div>



# 保存数据到新Excel


```python
tgi.to_excel('TGI.xlsx',index=False)
```


```python

```
本文数据来源@数据不吹牛
