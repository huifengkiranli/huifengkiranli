# Pivot-table for performance analysis

##Import data


```python
import pandas as pd 
import numpy as np
import os 
```


```python
os.chdir('/Users/hui2046/Downloads/SQL+Python/')
df = pd.read_csv('James_Harden.csv')
```

## Data info


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


## pivot_table: index


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
      <td>0.369
