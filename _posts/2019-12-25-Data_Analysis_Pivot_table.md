# KPI Analysis:Pivot-table

# Import data

```python
import pandas as pd 
import numpy as np
import os 
```


```python
os.chdir('/Users/hui2046/Downloads/SQL+Python/')
df = pd.read_csv('James_Harden.csv')
```

# Data info


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
      <th>对手</th>
      <th>胜负</th>
      <th>主客场</th>
      <th>命中</th>
      <th>投篮数</th>
      <th>投篮命中率</th>
      <th>3分命中率</th>
      <th>篮板</th>
      <th>助攻</th>
      <th>得分</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>勇士</td>
      <td>胜</td>
      <td>客</td>
      <td>10</td>
      <td>23</td>
      <td>0.435</td>
      <td>0.444</td>
      <td>6</td>
      <td>11</td>
      <td>27</td>
    </tr>
    <tr>
      <td>1</td>
      <td>国王</td>
      <td>胜</td>
      <td>客</td>
      <td>8</td>
      <td>21</td>
      <td>0.381</td>
      <td>0.286</td>
      <td>3</td>
      <td>9</td>
      <td>27</td>
    </tr>
    <tr>
      <td>2</td>
      <td>小牛</td>
      <td>胜</td>
      <td>主</td>
      <td>10</td>
      <td>19</td>
      <td>0.526</td>
      <td>0.462</td>
      <td>3</td>
      <td>7</td>
      <td>29</td>
    </tr>
    <tr>
      <td>3</td>
      <td>灰熊</td>
      <td>负</td>
      <td>主</td>
      <td>8</td>
      <td>20</td>
      <td>0.400</td>
      <td>0.250</td>
      <td>5</td>
      <td>8</td>
      <td>22</td>
    </tr>
    <tr>
      <td>4</td>
      <td>76人</td>
      <td>胜</td>
      <td>客</td>
      <td>10</td>
      <td>20</td>
      <td>0.500</td>
      <td>0.250</td>
      <td>3</td>
      <td>13</td>
      <td>27</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 25 entries, 0 to 24
    Data columns (total 10 columns):
    对手       25 non-null object
    胜负       25 non-null object
    主客场      25 non-null object
    命中       25 non-null int64
    投篮数      25 non-null int64
    投篮命中率    25 non-null float64
    3分命中率    25 non-null float64
    篮板       25 non-null int64
    助攻       25 non-null int64
    得分       25 non-null int64
    dtypes: float64(2), int64(5), object(3)
    memory usage: 2.1+ KB


# pivot_table: index


```python
# 查看harden对阵每个队的得分，index = ‘对手’

pd.pivot_table(df,index = '对手')
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
      <th>3分命中率</th>
      <th>助攻</th>
      <th>命中</th>
      <th>得分</th>
      <th>投篮命中率</th>
      <th>投篮数</th>
      <th>篮板</th>
    </tr>
    <tr>
      <th>对手</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>76人</td>
      <td>0.33950</td>
      <td>10.00</td>
      <td>9.0</td>
      <td>28.00</td>
      <td>0.4405</td>
      <td>20.5</td>
      <td>3.5</td>
    </tr>
    <tr>
      <td>勇士</td>
      <td>0.44400</td>
      <td>11.00</td>
      <td>10.0</td>
      <td>27.00</td>
      <td>0.4350</td>
      <td>23.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <td>国王</td>
      <td>0.28600</td>
      <td>9.00</td>
      <td>8.0</td>
      <td>27.00</td>
      <td>0.3810</td>
      <td>21.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>太阳</td>
      <td>0.54500</td>
      <td>7.00</td>
      <td>12.0</td>
      <td>48.00</td>
      <td>0.5450</td>
      <td>22.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>小牛</td>
      <td>0.46200</td>
      <td>7.00</td>
      <td>10.0</td>
      <td>29.00</td>
      <td>0.5260</td>
      <td>19.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>尼克斯</td>
      <td>0.36900</td>
      <td>9.50</td>
      <td>10.5</td>
      <td>34.00</td>
      <td>0.4175</td>
      <td>25.0</td>
      <td>3.5</td>
    </tr>
    <tr>
      <td>开拓者</td>
      <td>0.57100</td>
      <td>3.00</td>
      <td>16.0</td>
      <td>48.00</td>
      <td>0.5520</td>
      <td>29.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <td>掘金</td>
      <td>0.14300</td>
      <td>9.00</td>
      <td>6.0</td>
      <td>21.00</td>
      <td>0.3750</td>
      <td>16.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <td>步行者</td>
      <td>0.29150</td>
      <td>12.50</td>
      <td>8.5</td>
      <td>27.50</td>
      <td>0.3965</td>
      <td>21.5</td>
      <td>6.5</td>
    </tr>
    <tr>
      <td>湖人</td>
      <td>0.44400</td>
      <td>9.00</td>
      <td>13.0</td>
      <td>36.00</td>
      <td>0.5910</td>
      <td>22.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <td>灰熊</td>
      <td>0.35025</td>
      <td>7.75</td>
      <td>8.5</td>
      <td>27.25</td>
      <td>0.4015</td>
      <td>21.0</td>
      <td>4.5</td>
    </tr>
    <tr>
      <td>爵士</td>
      <td>0.60400</td>
      <td>8.00</td>
      <td>13.5</td>
      <td>42.50</td>
      <td>0.5905</td>
      <td>22.0</td>
      <td>3.5</td>
    </tr>
    <tr>
      <td>猛龙</td>
      <td>0.27300</td>
      <td>11.00</td>
      <td>8.0</td>
      <td>38.00</td>
      <td>0.3200</td>
      <td>25.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <td>篮网</td>
      <td>0.61500</td>
      <td>8.00</td>
      <td>13.0</td>
      <td>37.00</td>
      <td>0.6500</td>
      <td>20.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <td>老鹰</td>
      <td>0.54500</td>
      <td>11.00</td>
      <td>8.0</td>
      <td>29.00</td>
      <td>0.5330</td>
      <td>15.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>骑士</td>
      <td>0.42900</td>
      <td>13.00</td>
      <td>8.0</td>
      <td>35.00</td>
      <td>0.3810</td>
      <td>21.0</td>
      <td>11.0</td>
    </tr>
    <tr>
      <td>鹈鹕</td>
      <td>0.40000</td>
      <td>17.00</td>
      <td>8.0</td>
      <td>26.00</td>
      <td>0.5000</td>
      <td>16.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <td>黄蜂</td>
      <td>0.40000</td>
      <td>11.00</td>
      <td>8.0</td>
      <td>27.00</td>
      <td>0.4440</td>
      <td>18.0</td>
      <td>10.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#第二层索引，查看每个对手不同场次得分，index = ['对手','主客场']

pd.pivot_table(df,index = ['对手','主客场'])
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
      <th></th>
      <th>3分命中率</th>
      <th>助攻</th>
      <th>命中</th>
      <th>得分</th>
      <th>投篮命中率</th>
      <th>投篮数</th>
      <th>篮板</th>
    </tr>
    <tr>
      <th>对手</th>
      <th>主客场</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2" valign="top">76人</td>
      <td>主</td>
      <td>0.4290</td>
      <td>7.0</td>
      <td>8.0</td>
      <td>29.0</td>
      <td>0.381</td>
      <td>21.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <td>客</td>
      <td>0.2500</td>
      <td>13.0</td>
      <td>10.0</td>
      <td>27.0</td>
      <td>0.500</td>
      <td>20.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>勇士</td>
      <td>客</td>
      <td>0.4440</td>
      <td>11.0</td>
      <td>10.0</td>
      <td>27.0</td>
      <td>0.435</td>
      <td>23.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <td>国王</td>
      <td>客</td>
      <td>0.2860</td>
      <td>9.0</td>
      <td>8.0</td>
      <td>27.0</td>
      <td>0.381</td>
      <td>21.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>太阳</td>
      <td>客</td>
      <td>0.5450</td>
      <td>7.0</td>
      <td>12.0</td>
      <td>48.0</td>
      <td>0.545</td>
      <td>22.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>小牛</td>
      <td>主</td>
      <td>0.4620</td>
      <td>7.0</td>
      <td>10.0</td>
      <td>29.0</td>
      <td>0.526</td>
      <td>19.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td rowspan="2" valign="top">尼克斯</td>
      <td>主</td>
      <td>0.3850</td>
      <td>10.0</td>
      <td>12.0</td>
      <td>37.0</td>
      <td>0.444</td>
      <td>27.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>客</td>
      <td>0.3530</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>31.0</td>
      <td>0.391</td>
      <td>23.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <td>开拓者</td>
      <td>客</td>
      <td>0.5710</td>
      <td>3.0</td>
      <td>16.0</td>
      <td>48.0</td>
      <td>0.552</td>
      <td>29.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <td>掘金</td>
      <td>主</td>
      <td>0.1430</td>
      <td>9.0</td>
      <td>6.0</td>
      <td>21.0</td>
      <td>0.375</td>
      <td>16.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <td rowspan="2" valign="top">步行者</td>
      <td>主</td>
      <td>0.3330</td>
      <td>10.0</td>
      <td>8.0</td>
      <td>29.0</td>
      <td>0.364</td>
      <td>22.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <td>客</td>
      <td>0.2500</td>
      <td>15.0</td>
      <td>9.0</td>
      <td>26.0</td>
      <td>0.429</td>
      <td>21.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <td>湖人</td>
      <td>客</td>
      <td>0.4440</td>
      <td>9.0</td>
      <td>13.0</td>
      <td>36.0</td>
      <td>0.591</td>
      <td>22.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <td rowspan="2" valign="top">灰熊</td>
      <td>主</td>
      <td>0.3395</td>
      <td>8.0</td>
      <td>9.5</td>
      <td>30.0</td>
      <td>0.420</td>
      <td>22.5</td>
      <td>4.5</td>
    </tr>
    <tr>
      <td>客</td>
      <td>0.3610</td>
      <td>7.5</td>
      <td>7.5</td>
      <td>24.5</td>
      <td>0.383</td>
      <td>19.5</td>
      <td>4.5</td>
    </tr>
    <tr>
      <td rowspan="2" valign="top">爵士</td>
      <td>主</td>
      <td>0.8750</td>
      <td>13.0</td>
      <td>19.0</td>
      <td>56.0</td>
      <td>0.760</td>
      <td>25.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>客</td>
      <td>0.3330</td>
      <td>3.0</td>
      <td>8.0</td>
      <td>29.0</td>
      <td>0.421</td>
      <td>19.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <td>猛龙</td>
      <td>主</td>
      <td>0.2730</td>
      <td>11.0</td>
      <td>8.0</td>
      <td>38.0</td>
      <td>0.320</td>
      <td>25.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <td>篮网</td>
      <td>主</td>
      <td>0.6150</td>
      <td>8.0</td>
      <td>13.0</td>
      <td>37.0</td>
      <td>0.650</td>
      <td>20.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <td>老鹰</td>
      <td>客</td>
      <td>0.5450</td>
      <td>11.0</td>
      <td>8.0</td>
      <td>29.0</td>
      <td>0.533</td>
      <td>15.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>骑士</td>
      <td>主</td>
      <td>0.4290</td>
      <td>13.0</td>
      <td>8.0</td>
      <td>35.0</td>
      <td>0.381</td>
      <td>21.0</td>
      <td>11.0</td>
    </tr>
    <tr>
      <td>鹈鹕</td>
      <td>主</td>
      <td>0.4000</td>
      <td>17.0</td>
      <td>8.0</td>
      <td>26.0</td>
      <td>0.500</td>
      <td>16.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <td>黄蜂</td>
      <td>客</td>
      <td>0.4000</td>
      <td>11.0</td>
      <td>8.0</td>
      <td>27.0</td>
      <td>0.444</td>
      <td>18.0</td>
      <td>10.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 调换两个index顺序，index = ['主客场'，'对手']

pd.pivot_table(df, index = ['主客场','对手'])
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
      <th></th>
      <th>3分命中率</th>
      <th>助攻</th>
      <th>命中</th>
      <th>得分</th>
      <th>投篮命中率</th>
      <th>投篮数</th>
      <th>篮板</th>
    </tr>
    <tr>
      <th>主客场</th>
      <th>对手</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="11" valign="top">主</td>
      <td>76人</td>
      <td>0.4290</td>
      <td>7.0</td>
      <td>8.0</td>
      <td>29.0</td>
      <td>0.381</td>
      <td>21.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <td>小牛</td>
      <td>0.4620</td>
      <td>7.0</td>
      <td>10.0</td>
      <td>29.0</td>
      <td>0.526</td>
      <td>19.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>尼克斯</td>
      <td>0.3850</td>
      <td>10.0</td>
      <td>12.0</td>
      <td>37.0</td>
      <td>0.444</td>
      <td>27.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>掘金</td>
      <td>0.1430</td>
      <td>9.0</td>
      <td>6.0</td>
      <td>21.0</td>
      <td>0.375</td>
      <td>16.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <td>步行者</td>
      <td>0.3330</td>
      <td>10.0</td>
      <td>8.0</td>
      <td>29.0</td>
      <td>0.364</td>
      <td>22.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <td>灰熊</td>
      <td>0.3395</td>
      <td>8.0</td>
      <td>9.5</td>
      <td>30.0</td>
      <td>0.420</td>
      <td>22.5</td>
      <td>4.5</td>
    </tr>
    <tr>
      <td>爵士</td>
      <td>0.8750</td>
      <td>13.0</td>
      <td>19.0</td>
      <td>56.0</td>
      <td>0.760</td>
      <td>25.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>猛龙</td>
      <td>0.2730</td>
      <td>11.0</td>
      <td>8.0</td>
      <td>38.0</td>
      <td>0.320</td>
      <td>25.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <td>篮网</td>
      <td>0.6150</td>
      <td>8.0</td>
      <td>13.0</td>
      <td>37.0</td>
      <td>0.650</td>
      <td>20.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <td>骑士</td>
      <td>0.4290</td>
      <td>13.0</td>
      <td>8.0</td>
      <td>35.0</td>
      <td>0.381</td>
      <td>21.0</td>
      <td>11.0</td>
    </tr>
    <tr>
      <td>鹈鹕</td>
      <td>0.4000</td>
      <td>17.0</td>
      <td>8.0</td>
      <td>26.0</td>
      <td>0.500</td>
      <td>16.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <td rowspan="12" valign="top">客</td>
      <td>76人</td>
      <td>0.2500</td>
      <td>13.0</td>
      <td>10.0</td>
      <td>27.0</td>
      <td>0.500</td>
      <td>20.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>勇士</td>
      <td>0.4440</td>
      <td>11.0</td>
      <td>10.0</td>
      <td>27.0</td>
      <td>0.435</td>
      <td>23.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <td>国王</td>
      <td>0.2860</td>
      <td>9.0</td>
      <td>8.0</td>
      <td>27.0</td>
      <td>0.381</td>
      <td>21.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>太阳</td>
      <td>0.5450</td>
      <td>7.0</td>
      <td>12.0</td>
      <td>48.0</td>
      <td>0.545</td>
      <td>22.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>尼克斯</td>
      <td>0.3530</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>31.0</td>
      <td>0.391</td>
      <td>23.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <td>开拓者</td>
      <td>0.5710</td>
      <td>3.0</td>
      <td>16.0</td>
      <td>48.0</td>
      <td>0.552</td>
      <td>29.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <td>步行者</td>
      <td>0.2500</td>
      <td>15.0</td>
      <td>9.0</td>
      <td>26.0</td>
      <td>0.429</td>
      <td>21.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <td>湖人</td>
      <td>0.4440</td>
      <td>9.0</td>
      <td>13.0</td>
      <td>36.0</td>
      <td>0.591</td>
      <td>22.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <td>灰熊</td>
      <td>0.3610</td>
      <td>7.5</td>
      <td>7.5</td>
      <td>24.5</td>
      <td>0.383</td>
      <td>19.5</td>
      <td>4.5</td>
    </tr>
    <tr>
      <td>爵士</td>
      <td>0.3330</td>
      <td>3.0</td>
      <td>8.0</td>
      <td>29.0</td>
      <td>0.421</td>
      <td>19.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <td>老鹰</td>
      <td>0.5450</td>
      <td>11.0</td>
      <td>8.0</td>
      <td>29.0</td>
      <td>0.533</td>
      <td>15.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <td>黄蜂</td>
      <td>0.4000</td>
      <td>11.0</td>
      <td>8.0</td>
      <td>27.0</td>
      <td>0.444</td>
      <td>18.0</td>
      <td>10.0</td>
    </tr>
  </tbody>
</table>
</div>



# pivot_table: Values


```python
# Values对需要的数据进行筛选,values = '得分','助攻','篮板',切记[]

pd.pivot_table(df,index = ['主客场','胜负'],values = ['得分','助攻','篮板'])
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
      <th></th>
      <th>助攻</th>
      <th>得分</th>
      <th>篮板</th>
    </tr>
    <tr>
      <th>主客场</th>
      <th>胜负</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2" valign="top">主</td>
      <td>胜</td>
      <td>10.555556</td>
      <td>34.222222</td>
      <td>5.444444</td>
    </tr>
    <tr>
      <td>负</td>
      <td>8.666667</td>
      <td>29.666667</td>
      <td>5.000000</td>
    </tr>
    <tr>
      <td rowspan="2" valign="top">客</td>
      <td>胜</td>
      <td>9.000000</td>
      <td>32.000000</td>
      <td>4.916667</td>
    </tr>
    <tr>
      <td>负</td>
      <td>8.000000</td>
      <td>20.000000</td>
      <td>4.000000</td>
    </tr>
  </tbody>
</table>
</div>



# pivot_table: Aggfunc


```python
# 不同主客场和胜负的总（'得分','助攻','篮板'）和平均（'得分','助攻','篮板'，aggfunc=[np.sum,np.mean]

pd.pivot_table(df,index = ['主客场','胜负'],values = ['得分','助攻','篮板'],
               aggfunc=[np.sum,np.mean])
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
      <th colspan="3" halign="left">sum</th>
      <th colspan="3" halign="left">mean</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>助攻</th>
      <th>得分</th>
      <th>篮板</th>
      <th>助攻</th>
      <th>得分</th>
      <th>篮板</th>
    </tr>
    <tr>
      <th>主客场</th>
      <th>胜负</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2" valign="top">主</td>
      <td>胜</td>
      <td>95</td>
      <td>308</td>
      <td>49</td>
      <td>10.555556</td>
      <td>34.222222</td>
      <td>5.444444</td>
    </tr>
    <tr>
      <td>负</td>
      <td>26</td>
      <td>89</td>
      <td>15</td>
      <td>8.666667</td>
      <td>29.666667</td>
      <td>5.000000</td>
    </tr>
    <tr>
      <td rowspan="2" valign="top">客</td>
      <td>胜</td>
      <td>108</td>
      <td>384</td>
      <td>59</td>
      <td>9.000000</td>
      <td>32.000000</td>
      <td>4.916667</td>
    </tr>
    <tr>
      <td>负</td>
      <td>8</td>
      <td>20</td>
      <td>4</td>
      <td>8.000000</td>
      <td>20.000000</td>
      <td>4.000000</td>
    </tr>
  </tbody>
</table>
</div>



# pivot_table: Columns


```python
# columns类似index，用来设置列层次字段，不是必选，但可分割数据
# fill_value 填充空值，margins=true 或margins=1汇总数据

pd.pivot_table(df,index = ['主客场'],columns=['对手'],values=['得分'],aggfunc=[np.sum],
               fill_value=0,margins=True)
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
      <th colspan="19" halign="left">sum</th>
    </tr>
    <tr>
      <th></th>
      <th colspan="19" halign="left">得分</th>
    </tr>
    <tr>
      <th>对手</th>
      <th>76人</th>
      <th>勇士</th>
      <th>国王</th>
      <th>太阳</th>
      <th>小牛</th>
      <th>尼克斯</th>
      <th>开拓者</th>
      <th>掘金</th>
      <th>步行者</th>
      <th>湖人</th>
      <th>灰熊</th>
      <th>爵士</th>
      <th>猛龙</th>
      <th>篮网</th>
      <th>老鹰</th>
      <th>骑士</th>
      <th>鹈鹕</th>
      <th>黄蜂</th>
      <th>All</th>
    </tr>
    <tr>
      <th>主客场</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>主</td>
      <td>29</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>29</td>
      <td>37</td>
      <td>0</td>
      <td>21</td>
      <td>29</td>
      <td>0</td>
      <td>60</td>
      <td>56</td>
      <td>38</td>
      <td>37</td>
      <td>0</td>
      <td>35</td>
      <td>26</td>
      <td>0</td>
      <td>397</td>
    </tr>
    <tr>
      <td>客</td>
      <td>27</td>
      <td>27</td>
      <td>27</td>
      <td>48</td>
      <td>0</td>
      <td>31</td>
      <td>48</td>
      <td>0</td>
      <td>26</td>
      <td>36</td>
      <td>49</td>
      <td>29</td>
      <td>0</td>
      <td>0</td>
      <td>29</td>
      <td>0</td>
      <td>0</td>
      <td>27</td>
      <td>404</td>
    </tr>
    <tr>
      <td>All</td>
      <td>56</td>
      <td>27</td>
      <td>27</td>
      <td>48</td>
      <td>29</td>
      <td>68</td>
      <td>48</td>
      <td>21</td>
      <td>55</td>
      <td>36</td>
      <td>109</td>
      <td>85</td>
      <td>38</td>
      <td>37</td>
      <td>29</td>
      <td>35</td>
      <td>26</td>
      <td>27</td>
      <td>801</td>
    </tr>
  </tbody>
</table>
</div>




```python
table = pd.pivot_table(df,index = ['对手','胜负'],columns=['主客场'],values = ['得分','助攻','篮板'],
               aggfunc=[np.mean],fill_value=0)
table.info()
```

    <class 'pandas.core.frame.DataFrame'>
    MultiIndex: 20 entries, (76人, 胜) to (黄蜂, 胜)
    Data columns (total 6 columns):
    (mean, 助攻, 主)    20 non-null int64
    (mean, 助攻, 客)    20 non-null int64
    (mean, 得分, 主)    20 non-null int64
    (mean, 得分, 客)    20 non-null int64
    (mean, 篮板, 主)    20 non-null int64
    (mean, 篮板, 客)    20 non-null int64
    dtypes: int64(6)
    memory usage: 1.3+ KB



```python
table.head(20)
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
      <th colspan="6" halign="left">mean</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th colspan="2" halign="left">助攻</th>
      <th colspan="2" halign="left">得分</th>
      <th colspan="2" halign="left">篮板</th>
    </tr>
    <tr>
      <th></th>
      <th>主客场</th>
      <th>主</th>
      <th>客</th>
      <th>主</th>
      <th>客</th>
      <th>主</th>
      <th>客</th>
    </tr>
    <tr>
      <th>对手</th>
      <th>胜负</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2" valign="top">76人</td>
      <td>胜</td>
      <td>0</td>
      <td>13</td>
      <td>0</td>
      <td>27</td>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <td>负</td>
      <td>7</td>
      <td>0</td>
      <td>29</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <td>勇士</td>
      <td>胜</td>
      <td>0</td>
      <td>11</td>
      <td>0</td>
      <td>27</td>
      <td>0</td>
      <td>6</td>
    </tr>
    <tr>
      <td>国王</td>
      <td>胜</td>
      <td>0</td>
      <td>9</td>
      <td>0</td>
      <td>27</td>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <td>太阳</td>
      <td>胜</td>
      <td>0</td>
      <td>7</td>
      <td>0</td>
      <td>48</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <td>小牛</td>
      <td>胜</td>
      <td>7</td>
      <td>0</td>
      <td>29</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
    </tr>
    <tr>
      <td>尼克斯</td>
      <td>胜</td>
      <td>10</td>
      <td>9</td>
      <td>37</td>
      <td>31</td>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <td>开拓者</td>
      <td>胜</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>48</td>
      <td>0</td>
      <td>8</td>
    </tr>
    <tr>
      <td>掘金</td>
      <td>胜</td>
      <td>9</td>
      <td>0</td>
      <td>21</td>
      <td>0</td>
      <td>8</td>
      <td>0</td>
    </tr>
    <tr>
      <td>步行者</td>
      <td>胜</td>
      <td>10</td>
      <td>15</td>
      <td>29</td>
      <td>26</td>
      <td>8</td>
      <td>5</td>
    </tr>
    <tr>
      <td>湖人</td>
      <td>胜</td>
      <td>0</td>
      <td>9</td>
      <td>0</td>
      <td>36</td>
      <td>0</td>
      <td>4</td>
    </tr>
    <tr>
      <td rowspan="2" valign="top">灰熊</td>
      <td>胜</td>
      <td>8</td>
      <td>7</td>
      <td>38</td>
      <td>29</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <td>负</td>
      <td>8</td>
      <td>8</td>
      <td>22</td>
      <td>20</td>
      <td>5</td>
      <td>4</td>
    </tr>
    <tr>
      <td>爵士</td>
      <td>胜</td>
      <td>13</td>
      <td>3</td>
      <td>56</td>
      <td>29</td>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <td>猛龙</td>
      <td>负</td>
      <td>11</td>
      <td>0</td>
      <td>38</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
    </tr>
    <tr>
      <td>篮网</td>
      <td>胜</td>
      <td>8</td>
      <td>0</td>
      <td>37</td>
      <td>0</td>
      <td>10</td>
      <td>0</td>
    </tr>
    <tr>
      <td>老鹰</td>
      <td>胜</td>
      <td>0</td>
      <td>11</td>
      <td>0</td>
      <td>29</td>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <td>骑士</td>
      <td>胜</td>
      <td>13</td>
      <td>0</td>
      <td>35</td>
      <td>0</td>
      <td>11</td>
      <td>0</td>
    </tr>
    <tr>
      <td>鹈鹕</td>
      <td>胜</td>
      <td>17</td>
      <td>0</td>
      <td>26</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <td>黄蜂</td>
      <td>胜</td>
      <td>0</td>
      <td>11</td>
      <td>0</td>
      <td>27</td>
      <td>0</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
