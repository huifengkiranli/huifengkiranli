# Airbnb运营分析：用户画像，用户行为及渠道分析
本文针对Airbnb在Kaggle提供的真实产品运营数据，对产品运营和用户画像做数据分析(Python&SQL)，运用Tableau形成可视化报告和Dashboard，为运营和营销管理改进提供数据支持。
<br>文章包括两部分：
<br> 一. **可视化运营分析和建议报告:** 
<br>1. 用户画像分析
<br> 2. 渠道推广分析
<br> 3. 转化漏斗分析
<br> 4. 分析总结
<br> 5. 产品和运营管理建议
<br> 二. **Python和SQL数据清洗和分析过程**

<br> **Airbnb基本介绍：**Airbnb成立于2008年，并已经成为了短租民宿行业的巨头，其业务遍布了191个国家。作为一款社区平台类产品，Airbnb在建立了良好的产品体验、房源美感、民宿共享服务之后，这款产品和背后的服务还有哪些需要改进的地方？
<br> **运营管理问题：**针对分析的目的，提出以下三个问题：
<br>（1）用户特征：Airbnb的目标用户群体具有什么样的特征？
<br>（2）渠道效果：Airbnb当前的推广渠道有哪些是优质的、有哪些做的还不够好且需要改进？
<br>（3）运营管理改进：当前的转化率和流失率中哪些环节存在问题，或者有较大的改进空间？


# 一. Airbnb运营分析报告
## 1. User Profile 用户画像分析
![](https://kiranli.github.io/images/a1.png)
![](https://kiranli.github.io/images/a2.png)
![](https://kiranli.github.io/images/a3.png)
![](https://kiranli.github.io/images/a4.png)
![](https://kiranli.github.io/images/a5.png)

## 2. Channel Marketing Analysis 渠道推广分析
![](https://kiranli.github.io/images/a8.png)
![](https://kiranli.github.io/images/a6.png)
![](https://kiranli.github.io/images/a7.png)
![](https://kiranli.github.io/images/a9.png)

<br> **Interactive Dashboard**
<br> Tableau建立动态化的工作台，方便以全局来检查分析是否有环节遗漏。
![](https://kiranli.github.io/images/a10.png)

## 3. Funnel Analysis 转化漏斗分析
**Funnel analysis** is a powerful analytics method that shows the conversion between the most important steps of the user journey. Funnels are an extremely useful and helpful data tool that can provide you a great overview about your product. In a nutshell, funnels are representing several events your users perform one after another. Calculating how many unique users made each event could show you a conversion rate between each step, so you could actually localize a problem down to a certain stage.
<br> **AARRR Funnel Framework：** 在AARRR Funnel Framework工作框架中，第一个A是Acquire，即用户获取，提高新用户获取的数量和质量是非常重要的，需要不断监测并优化的一个工作，哪些渠道的推广效果更好，企业就要及时调整和增加此渠道的投入，哪些渠道的效果很差，就要及时查找原因并给出解决。
<br>**转化漏斗分析**也是数据分析环节的重要指标，可以从宏观角度了解整个产品的业务转化情况，企业针对流失率较高的漏斗环节进行改进，可以有效促进业务发展。
![](https://kiranli.github.io/images/a11.png)

## 4. 分析总结
### （1). User Profile 用户画像总结

* 用户性别: 男性用户多于女性用户，但是差别不大, 约7%；
* 用户年龄：以中青年为主，用户数量最多的是30岁～39岁，其次为20～29岁，然后为40～49岁;
* 用户分布地区：最多的为欧美地区，其次是中国，但欧美占比达到了90%以上（截止2014年）,中国用户预订的最多的其他国家是美国，占比高达90%以上(国家部分数据太大Tableau无法可视化呈现）。
### （2). Marketing Channel 流量渠道总结

* 苹果设备用户居多，多余Windows和安卓用户；
* 前期（2011年之前）平缓，2012年1月之后开始快速增长；
* 6～10月和1月是旅行旺季，也是Airbnb用户增长的旺季；
* drict（直接应用市场下载注册）的注册量最多，占总注册量的64.38%。
注册量排名前七的渠道，占据了产品全部渠道注册来源数量的90%以上;
* **效果不好的渠道**：
<br> content_google的转化率异常，明显低于全渠道转化率的均值;
<br> api_other（其他产品的API对接）渠道的转化率也比较低;
<br> content（内容推广）这种推广方式下各渠道的转化率都很低；
<br> sem中sem-non-brand_bing、sem-non-brand_vast两种SEM渠道的转化率都偏低。
* **效果好的渠道**：
<br> seo_google的注册量和转化率表现均很好；
<br> sem_brand_google的注册量可转化率表现很好，是付费渠道。
* **营销内容方面：**
<br> Untracked占比大，数据追踪环节出现问题；
<br> linked和product两个营销内容的的转化率好；local ops的转化率非常低。
### （3). Funnel Part 转化漏斗总结
* 流失率最高的环节: 用户注册到下单，仅有14%的注册用户下单；
* 下单用户中有大约13%的用户最终没有支付成功；
* 活跃和复购环节表现良好，说明Airbnb的产品和服务好，老用户黏性高。

## 5. 业务和产品上的建议

### （1). User Profile-锁定目标用户群

根据年龄分布特征，建议SEO或者付费广告投放时，投放对象细化至年龄在20～39岁用户，加大对苹果用户的营销。

### （2). Marketing Channel 推广渠道改进

* 建议运营部门在每年的7～10月，1月加大活动营销的力度，加大渠道广告的投放力度；
* 在主要渠道中：content_google非常低（约15%），建议运营部门计算此渠道的ROI和ARPU（每客户平均收入），如果ROI > ARPU，建议停止此渠道的投放；api_other（其他产品的API对接）渠道的转化率较低，建议产品设计部查找尾部排名的API对接产品，与对方产品沟通，从产品的流程设计、交互设计角度查找原因；
* **SEO**推广下各渠道的拉新和转化都好，SEO作为一种较低成本的获客方式（主要为人力成本），建议企业管理层日常要更加支持SEO相关的资源投入，甚至考虑扩大SEO的团队。
* 不同营销内容的拉新和转化效果也不同，有优秀营销内容linked和product，和表现较差local ops。针对local ops, 如果仍在活动过程中，建议对内容优化或更换；如果是活动已结束，运营部门应针对不同质量的营销内容做对比分析，总结内容策划上的方法论，便于之后的实践。
* 营销内容的埋点统计效果很差，常见两方面的原因。如果是技术研发导致的统计功能出错，需立即修复。如果是运营人员不注重这一块的统计，没有提出埋点的任务，则需要行政介入，要求之后做好埋点工作。
### （3). Funnel Advice 转化漏斗方面

* **提高下单转化率：**注册用户到下单用户是airbnb转化漏斗中流失率最高的一个环节，仅有14%的注册用户下单。此环节作为企业营收的主要来源之一，建议围绕提高下单率做更多的工作，例如针对活跃用户的用户轨迹定期推送（产品push+短信邮件）优质房源，这是一项长期工作；
* 下单用户中有大约13%的用户最终没有支付，需要了解具体原因，建议进行用户调研、或者在产品上统计用户未支付原因，是用户自身决策导致、还是产品流程的原因、还是支付类型不满足个别地区等。

# 二. Python和SQL数据清洗和分析


## 1. Data preparation


```python
import pandas as pd 
import numpy as np
import os 
```


```python
os.chdir('/Users/hui2046/Downloads/SQL+Python/Airbnb_data')
train_users = pd.read_csv('train_users_2.csv')
test_users = pd.read_csv('test_users.csv')
```

## 2.Data information


```python
train_users.info()
train_users.head(10)
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 213451 entries, 0 to 213450
    Data columns (total 16 columns):
    id                         213451 non-null object
    date_account_created       213451 non-null object
    timestamp_first_active     213451 non-null int64
    date_first_booking         88908 non-null object
    gender                     213451 non-null object
    age                        125461 non-null float64
    signup_method              213451 non-null object
    signup_flow                213451 non-null int64
    language                   213451 non-null object
    affiliate_channel          213451 non-null object
    affiliate_provider         213451 non-null object
    first_affiliate_tracked    207386 non-null object
    signup_app                 213451 non-null object
    first_device_type          213451 non-null object
    first_browser              213451 non-null object
    country_destination        213451 non-null object
    dtypes: float64(1), int64(2), object(13)
    memory usage: 26.1+ MB





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
      <th>id</th>
      <th>date_account_created</th>
      <th>timestamp_first_active</th>
      <th>date_first_booking</th>
      <th>gender</th>
      <th>age</th>
      <th>signup_method</th>
      <th>signup_flow</th>
      <th>language</th>
      <th>affiliate_channel</th>
      <th>affiliate_provider</th>
      <th>first_affiliate_tracked</th>
      <th>signup_app</th>
      <th>first_device_type</th>
      <th>first_browser</th>
      <th>country_destination</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>gxn3p5htnn</td>
      <td>2010-06-28</td>
      <td>20090319043255</td>
      <td>NaN</td>
      <td>-unknown-</td>
      <td>NaN</td>
      <td>facebook</td>
      <td>0</td>
      <td>en</td>
      <td>direct</td>
      <td>direct</td>
      <td>untracked</td>
      <td>Web</td>
      <td>Mac Desktop</td>
      <td>Chrome</td>
      <td>NDF</td>
    </tr>
    <tr>
      <td>1</td>
      <td>820tgsjxq7</td>
      <td>2011-05-25</td>
      <td>20090523174809</td>
      <td>NaN</td>
      <td>MALE</td>
      <td>38.0</td>
      <td>facebook</td>
      <td>0</td>
      <td>en</td>
      <td>seo</td>
      <td>google</td>
      <td>untracked</td>
      <td>Web</td>
      <td>Mac Desktop</td>
      <td>Chrome</td>
      <td>NDF</td>
    </tr>
    <tr>
      <td>2</td>
      <td>4ft3gnwmtx</td>
      <td>2010-09-28</td>
      <td>20090609231247</td>
      <td>2010-08-02</td>
      <td>FEMALE</td>
      <td>56.0</td>
      <td>basic</td>
      <td>3</td>
      <td>en</td>
      <td>direct</td>
      <td>direct</td>
      <td>untracked</td>
      <td>Web</td>
      <td>Windows Desktop</td>
      <td>IE</td>
      <td>US</td>
    </tr>
    <tr>
      <td>3</td>
      <td>bjjt8pjhuk</td>
      <td>2011-12-05</td>
      <td>20091031060129</td>
      <td>2012-09-08</td>
      <td>FEMALE</td>
      <td>42.0</td>
      <td>facebook</td>
      <td>0</td>
      <td>en</td>
      <td>direct</td>
      <td>direct</td>
      <td>untracked</td>
      <td>Web</td>
      <td>Mac Desktop</td>
      <td>Firefox</td>
      <td>other</td>
    </tr>
    <tr>
      <td>4</td>
      <td>87mebub9p4</td>
      <td>2010-09-14</td>
      <td>20091208061105</td>
      <td>2010-02-18</td>
      <td>-unknown-</td>
      <td>41.0</td>
      <td>basic</td>
      <td>0</td>
      <td>en</td>
      <td>direct</td>
      <td>direct</td>
      <td>untracked</td>
      <td>Web</td>
      <td>Mac Desktop</td>
      <td>Chrome</td>
      <td>US</td>
    </tr>
    <tr>
      <td>5</td>
      <td>osr2jwljor</td>
      <td>2010-01-01</td>
      <td>20100101215619</td>
      <td>2010-01-02</td>
      <td>-unknown-</td>
      <td>NaN</td>
      <td>basic</td>
      <td>0</td>
      <td>en</td>
      <td>other</td>
      <td>other</td>
      <td>omg</td>
      <td>Web</td>
      <td>Mac Desktop</td>
      <td>Chrome</td>
      <td>US</td>
    </tr>
    <tr>
      <td>6</td>
      <td>lsw9q7uk0j</td>
      <td>2010-01-02</td>
      <td>20100102012558</td>
      <td>2010-01-05</td>
      <td>FEMALE</td>
      <td>46.0</td>
      <td>basic</td>
      <td>0</td>
      <td>en</td>
      <td>other</td>
      <td>craigslist</td>
      <td>untracked</td>
      <td>Web</td>
      <td>Mac Desktop</td>
      <td>Safari</td>
      <td>US</td>
    </tr>
    <tr>
      <td>7</td>
      <td>0d01nltbrs</td>
      <td>2010-01-03</td>
      <td>20100103191905</td>
      <td>2010-01-13</td>
      <td>FEMALE</td>
      <td>47.0</td>
      <td>basic</td>
      <td>0</td>
      <td>en</td>
      <td>direct</td>
      <td>direct</td>
      <td>omg</td>
      <td>Web</td>
      <td>Mac Desktop</td>
      <td>Safari</td>
      <td>US</td>
    </tr>
    <tr>
      <td>8</td>
      <td>a1vcnhxeij</td>
      <td>2010-01-04</td>
      <td>20100104004211</td>
      <td>2010-07-29</td>
      <td>FEMALE</td>
      <td>50.0</td>
      <td>basic</td>
      <td>0</td>
      <td>en</td>
      <td>other</td>
      <td>craigslist</td>
      <td>untracked</td>
      <td>Web</td>
      <td>Mac Desktop</td>
      <td>Safari</td>
      <td>US</td>
    </tr>
    <tr>
      <td>9</td>
      <td>6uh8zyj2gn</td>
      <td>2010-01-04</td>
      <td>20100104023758</td>
      <td>2010-01-04</td>
      <td>-unknown-</td>
      <td>46.0</td>
      <td>basic</td>
      <td>0</td>
      <td>en</td>
      <td>other</td>
      <td>craigslist</td>
      <td>omg</td>
      <td>Web</td>
      <td>Mac Desktop</td>
      <td>Firefox</td>
      <td>US</td>
    </tr>
  </tbody>
</table>
</div>



可见数据总量为213451行，16个字段，数据缺失数量较多。专业字段解释：
<br/> date_account_created：the date of account creation 帐户创建日期
<br/> date_first_booking：date of first booking 首次预订的日期
<br/> signup_method：注册方式
<br/> signup_flow：the page a user came to signup up from 用户注册的页面
<br/> affiliate_channel：what kind of paid marketing 营销方式
<br/> affiliate_provider：where the marketing is e.g. google, craigslist, other 营销来源，例如google，craigslist，其他
<br/> first_affiliate_tracked：whats the first marketing the user interacted with before the signing up 在注册之前，用户与之交互的第一个营销广告是什么。
<br/> destination country: 目的地国家 There are 12 possible outcomes of the destination country: 'US', 'FR', 'CA', 'GB', 'ES', 'IT', 'PT', 'NL','DE', 'AU', 'NDF' (no destination found), and 'other'. Please note that 'NDF' is different from 'other' because 'other' means there was a booking, but is to a country not included in the list, while 'NDF' means there wasn't a booking.




```python
test_users.info()
test_users.head(10)
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 62096 entries, 0 to 62095
    Data columns (total 15 columns):
    id                         62096 non-null object
    date_account_created       62096 non-null object
    timestamp_first_active     62096 non-null int64
    date_first_booking         0 non-null float64
    gender                     62096 non-null object
    age                        33220 non-null float64
    signup_method              62096 non-null object
    signup_flow                62096 non-null int64
    language                   62096 non-null object
    affiliate_channel          62096 non-null object
    affiliate_provider         62096 non-null object
    first_affiliate_tracked    62076 non-null object
    signup_app                 62096 non-null object
    first_device_type          62096 non-null object
    first_browser              62096 non-null object
    dtypes: float64(2), int64(2), object(11)
    memory usage: 7.1+ MB





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
      <th>id</th>
      <th>date_account_created</th>
      <th>timestamp_first_active</th>
      <th>date_first_booking</th>
      <th>gender</th>
      <th>age</th>
      <th>signup_method</th>
      <th>signup_flow</th>
      <th>language</th>
      <th>affiliate_channel</th>
      <th>affiliate_provider</th>
      <th>first_affiliate_tracked</th>
      <th>signup_app</th>
      <th>first_device_type</th>
      <th>first_browser</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>5uwns89zht</td>
      <td>2014-07-01</td>
      <td>20140701000006</td>
      <td>NaN</td>
      <td>FEMALE</td>
      <td>35.0</td>
      <td>facebook</td>
      <td>0</td>
      <td>en</td>
      <td>direct</td>
      <td>direct</td>
      <td>untracked</td>
      <td>Moweb</td>
      <td>iPhone</td>
      <td>Mobile Safari</td>
    </tr>
    <tr>
      <td>1</td>
      <td>jtl0dijy2j</td>
      <td>2014-07-01</td>
      <td>20140701000051</td>
      <td>NaN</td>
      <td>-unknown-</td>
      <td>NaN</td>
      <td>basic</td>
      <td>0</td>
      <td>en</td>
      <td>direct</td>
      <td>direct</td>
      <td>untracked</td>
      <td>Moweb</td>
      <td>iPhone</td>
      <td>Mobile Safari</td>
    </tr>
    <tr>
      <td>2</td>
      <td>xx0ulgorjt</td>
      <td>2014-07-01</td>
      <td>20140701000148</td>
      <td>NaN</td>
      <td>-unknown-</td>
      <td>NaN</td>
      <td>basic</td>
      <td>0</td>
      <td>en</td>
      <td>direct</td>
      <td>direct</td>
      <td>linked</td>
      <td>Web</td>
      <td>Windows Desktop</td>
      <td>Chrome</td>
    </tr>
    <tr>
      <td>3</td>
      <td>6c6puo6ix0</td>
      <td>2014-07-01</td>
      <td>20140701000215</td>
      <td>NaN</td>
      <td>-unknown-</td>
      <td>NaN</td>
      <td>basic</td>
      <td>0</td>
      <td>en</td>
      <td>direct</td>
      <td>direct</td>
      <td>linked</td>
      <td>Web</td>
      <td>Windows Desktop</td>
      <td>IE</td>
    </tr>
    <tr>
      <td>4</td>
      <td>czqhjk3yfe</td>
      <td>2014-07-01</td>
      <td>20140701000305</td>
      <td>NaN</td>
      <td>-unknown-</td>
      <td>NaN</td>
      <td>basic</td>
      <td>0</td>
      <td>en</td>
      <td>direct</td>
      <td>direct</td>
      <td>untracked</td>
      <td>Web</td>
      <td>Mac Desktop</td>
      <td>Safari</td>
    </tr>
    <tr>
      <td>5</td>
      <td>szx28ujmhf</td>
      <td>2014-07-01</td>
      <td>20140701000336</td>
      <td>NaN</td>
      <td>FEMALE</td>
      <td>28.0</td>
      <td>basic</td>
      <td>0</td>
      <td>en</td>
      <td>sem-brand</td>
      <td>google</td>
      <td>omg</td>
      <td>Web</td>
      <td>Windows Desktop</td>
      <td>Chrome</td>
    </tr>
    <tr>
      <td>6</td>
      <td>guenkfjcbq</td>
      <td>2014-07-01</td>
      <td>20140701000514</td>
      <td>NaN</td>
      <td>MALE</td>
      <td>48.0</td>
      <td>basic</td>
      <td>25</td>
      <td>en</td>
      <td>direct</td>
      <td>direct</td>
      <td>untracked</td>
      <td>iOS</td>
      <td>iPhone</td>
      <td>-unknown-</td>
    </tr>
    <tr>
      <td>7</td>
      <td>tkpq0mlugk</td>
      <td>2014-07-01</td>
      <td>20140701000649</td>
      <td>NaN</td>
      <td>-unknown-</td>
      <td>NaN</td>
      <td>basic</td>
      <td>0</td>
      <td>en</td>
      <td>direct</td>
      <td>direct</td>
      <td>untracked</td>
      <td>Web</td>
      <td>Mac Desktop</td>
      <td>Chrome</td>
    </tr>
    <tr>
      <td>8</td>
      <td>3xtgd5p9dn</td>
      <td>2014-07-01</td>
      <td>20140701000837</td>
      <td>NaN</td>
      <td>-unknown-</td>
      <td>NaN</td>
      <td>basic</td>
      <td>0</td>
      <td>en</td>
      <td>direct</td>
      <td>direct</td>
      <td>untracked</td>
      <td>Web</td>
      <td>Mac Desktop</td>
      <td>Chrome</td>
    </tr>
    <tr>
      <td>9</td>
      <td>md9aj22l5a</td>
      <td>2014-07-01</td>
      <td>20140701002245</td>
      <td>NaN</td>
      <td>-unknown-</td>
      <td>NaN</td>
      <td>basic</td>
      <td>0</td>
      <td>en</td>
      <td>sem-non-brand</td>
      <td>google</td>
      <td>omg</td>
      <td>Web</td>
      <td>Windows Desktop</td>
      <td>Firefox</td>
    </tr>
  </tbody>
</table>
</div>



可见测试数据总量为62096行，15个字段，专业字段解释：
<br/> timestamp_first_active: timestamp of the first activity, note that it can be earlier than date_account_created or date_first_booking because a user can search before signing up 第一次活跃时间，可能早于账户建立账户和第一次预定的时间，因为未注册前浏览网站。

## 3.建立关联表 .concat()


```python
# 由于要把两张表train_users1和test_users合并，因此需要删除train_users1的多余字段country_destination列；
# axis = 1是删除列，默认是axis=0

train_users1 = train_users.drop(["country_destination"],axis =1)
```


```python
all_users1 = pd.concat([train_users1,test_users])
