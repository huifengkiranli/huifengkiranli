# Operations Analysis运营分析之Airbnb
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
##1. User Profile 用户画像分析
![](https://kiranli.github.io/images/a1.png)
![](https://kiranli.github.io/images/a1.png)
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
###（1). User Profile 用户画像总结

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
###（3). Funnel Part 转化漏斗总结
* 流失率最高的环节: 用户注册到下单，仅有14%的注册用户下单；
* 下单用户中有大约13%的用户最终没有支付成功；
* 活跃和复购环节表现良好，说明Airbnb的产品和服务好，老用户黏性高。

## 5. 业务和产品上的建议

###（1). User Profile-锁定目标用户群

根据年龄分布特征，建议SEO或者付费广告投放时，投放对象细化至年龄在20～39岁用户，加大对苹果用户的营销。

###（2). Marketing Channel 推广渠道改进

* 建议运营部门在每年的7～10月，1月加大活动营销的力度，加大渠道广告的投放力度；
* 在主要渠道中：content_google非常低（约15%），建议运营部门计算此渠道的ROI和ARPU（每客户平均收入），如果ROI > ARPU，建议停止此渠道的投放；api_other（其他产品的API对接）渠道的转化率较低，建议产品设计部查找尾部排名的API对接产品，与对方产品沟通，从产品的流程设计、交互设计角度查找原因；
* **SEO**推广下各渠道的拉新和转化都好，SEO作为一种较低成本的获客方式（主要为人力成本），建议企业管理层日常要更加支持SEO相关的资源投入，甚至考虑扩大SEO的团队。
* 不同营销内容的拉新和转化效果也不同，有优秀营销内容linked和product，和表现较差local ops。针对local ops, 如果仍在活动过程中，建议对内容优化或更换；如果是活动已结束，运营部门应针对不同质量的营销内容做对比分析，总结内容策划上的方法论，便于之后的实践。
* 营销内容的埋点统计效果很差，常见两方面的原因。如果是技术研发导致的统计功能出错，需立即修复。如果是运营人员不注重这一块的统计，没有提出埋点的任务，则需要行政介入，要求之后做好埋点工作。
### （3). Funnel Advice 转化漏斗方面

* **提高下单转化率：**注册用户到下单用户是airbnb转化漏斗中流失率最高的一个环节，仅有14%的注册用户下单。此环节作为企业营收的主要来源之一，建议围绕提高下单率做更多的工作，例如针对活跃用户的用户轨迹定期推送（产品push+短信邮件）优质房源，这是一项长期工作；
* 下单用户中有大约13%的用户最终没有支付，需要了解具体原因，建议进行用户调研、或者在产品上统计用户未支付原因，是用户自身决策导致、还是产品流程的原因、还是支付类型不满足个别地区等。

# 二. Python和SQL数据清洗和分析


##1. Data preparation


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
all_users1.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 275547 entries, 0 to 62095
    Data columns (total 15 columns):
    id                         275547 non-null object
    date_account_created       275547 non-null object
    timestamp_first_active     275547 non-null int64
    date_first_booking         88908 non-null object
    gender                     275547 non-null object
    age                        158681 non-null float64
    signup_method              275547 non-null object
    signup_flow                275547 non-null int64
    language                   275547 non-null object
    affiliate_channel          275547 non-null object
    affiliate_provider         275547 non-null object
    first_affiliate_tracked    269462 non-null object
    signup_app                 275547 non-null object
    first_device_type          275547 non-null object
    first_browser              275547 non-null object
    dtypes: float64(1), int64(2), object(12)
    memory usage: 33.6+ MB


## 4.缺失值处理


由info（）查询可知，存在缺失值的字段有：date_first_booking, age, first_affiliate_tracked.
<br/> 分析缺失原因：
<br/> date_first_booking，即首次预定时间，这数据如果缺失，在业务上可以理解为此用户为“未预定用户”，也就是浏览网站但没有下单的用户。
<br/> 年龄由于这部分信息是选填的，空值表明用户未填写。
<br/> first_affiliate_tracked为空值是由于前端统计时数据没有统计到。
<br/> 实际分析中是需要结合业务特点和分析对缺失值做删除.dropna()或填充.fillna()，本文不做处理。

## 5.异常值查询


```python
all_users1.describe()
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
      <th>timestamp_first_active</th>
      <th>age</th>
      <th>signup_flow</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>count</td>
      <td>2.755470e+05</td>
      <td>158681.000000</td>
      <td>275547.000000</td>
    </tr>
    <tr>
      <td>mean</td>
      <td>2.013310e+13</td>
      <td>47.145310</td>
      <td>4.291965</td>
    </tr>
    <tr>
      <td>std</td>
      <td>9.146438e+09</td>
      <td>142.629468</td>
      <td>8.794313</td>
    </tr>
    <tr>
      <td>min</td>
      <td>2.009032e+13</td>
      <td>1.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <td>25%</td>
      <td>2.013040e+13</td>
      <td>28.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <td>50%</td>
      <td>2.014010e+13</td>
      <td>33.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <td>75%</td>
      <td>2.014062e+13</td>
      <td>42.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <td>max</td>
      <td>2.014093e+13</td>
      <td>2014.000000</td>
      <td>25.000000</td>
    </tr>
  </tbody>
</table>
</div>



看到age年龄字段最小值有1岁，最大值有2014岁，为异常值,年龄分析中需注意。

## 6.重复值处理


```python
# 因为每个用户只生成一条记录，所以应删除id有重复的

all_users1 = all_users1.drop_duplicates('id')
```

# 用户画像分析

## 1.用户性别


```python
all_users1['gender'].value_counts()
```




    -unknown-    129480
    FEMALE        77524
    MALE          68209
    OTHER           334
    Name: gender, dtype: int64



可见用户中男女性别数量占比差距不大，女性用户要比男性用户多9315人。

## 2.年龄分布


```python
# 按年龄分组统计每个年龄的人数
bins = [10,19,29,39,49,59,69,80]
labels = ['10s','20s','30s','40s','50s','60s','70s']
all_users1['age_by_decade'] = pd.cut(x=all_users1['age'],
                                     bins = [10,19,29,39,49,59,69,80],
                                     right=False,
                                     labels=['10s','20s','30s','40s','50s','60s','70s'])
all_users1['age_by_decade'].value_counts()
```




    30s    62603
    20s    43152
    40s    26639
    50s    13461
    60s     6770
    70s     1803
    10s      953
    Name: age_by_decade, dtype: int64



airbnb的用户主要为“中青年群体”，其中用户数量最多的是20岁到40岁，占比约70%。

## 3.使用设备分布


```python
all_users1['first_device_type'].value_counts()
```




    Mac Desktop           106328
    Windows Desktop        86948
    iPhone                 39814
    iPad                   18036
    Other/Unknown          11167
    Android Phone           9458
    Android Tablet          2098
    Desktop (Other)         1507
    SmartPhone (Other)       191
    Name: first_device_type, dtype: int64



整体上，airbnb用户登陆设备中：电脑端Mac比windows多，移动端iPhone和iPad比Android多，这是用户的一大特征，苹果用户居多。


```python
# 不同年龄段使用设备偏好
age_dev = all_users1.groupby('age_by_decade')['first_device_type'].value_counts()
age_dev 
```




    age_by_decade  first_device_type 
    10s            Mac Desktop           381
                   Windows Desktop       356
                   iPhone                113
                   iPad                   59
                   Other/Unknown          18
                                        ... 
    70s            Other/Unknown          41
                   Android Tablet         22
                   Android Phone          11
                   Desktop (Other)         6
                   SmartPhone (Other)      1
    Name: first_device_type, Length: 63, dtype: int64



## 4.用户语言偏好


```python
all_users1['language'].value_counts()
```




    en           265538
    zh             2634
    fr             1508
    es             1174
    ko             1116
    de              977
    it              633
    ru              508
    ja              345
    pt              322
    sv              176
    nl              134
    tr               92
    da               75
    pl               75
    no               51
    cs               49
    el               30
    th               28
    hu               25
    id               23
    fi               20
    ca                6
    is                5
    hr                2
    -unknown-         1
    Name: language, dtype: int64




```python
# 不同年龄段语言偏好
age_lan = all_users1.groupby('age_by_decade')['language'].value_counts()
age_lan
```




    age_by_decade  language
    10s            en          830
                   fr           40
                   es           17
                   ru           13
                   it           10
                              ... 
    70s            ru            3
                   de            2
                   ja            2
                   cs            1
                   tr            1
    Name: language, Length: 137, dtype: int64



## 5.各种语言的目的地国家偏好


```python
#NDF：no destination found,所以统计各种语言下的国家偏好数量时，删除掉NDF的栏
train_users_no_NDF = train_users.loc[train_users['country_destination']!='NDF']

#groupby(language)[' '].value_counts()
lan_coun = train_users_no_NDF.groupby('language')['country_destination'].value_counts()
lan_coun
```




    language  country_destination
    ca        US                      2
    cs        US                      6
              other                   2
              ES                      1
    da        US                     14
                                     ..
    zh        IT                      5
              ES                      3
              AU                      2
              CA                      2
              DE                      2
    Name: country_destination, Length: 133, dtype: int64



# 推广渠道分析

## 1.每月用户新增分析


```python
all_users1.head()
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
      <th>age_by_decade</th>
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
      <td>NaN</td>
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
      <td>30s</td>
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
      <td>50s</td>
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
      <td>40s</td>
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
      <td>40s</td>
    </tr>
  </tbody>
</table>
</div>




```python
#日期格式为yyyy-mm-dd,因为统计月新增，所以只取前7个字符，.str[:7]
all_users1['y_m'] = all_users1['date_account_created'].str[:7]
date_account_created = all_users1.groupby('y_m')['id'].count()
date_account_created
```




    y_m
    2010-01       61
    2010-02      102
    2010-03      163
    2010-04      157
    2010-05      227
    2010-06      222
    2010-07      307
    2010-08      312
    2010-09      371
    2010-10      309
    2010-11      286
    2010-12      271
    2011-01      316
    2011-02      362
    2011-03      491
    2011-04      577
    2011-05      744
    2011-06      822
    2011-07      993
    2011-08     1454
    2011-09     1864
    2011-10     1477
    2011-11     1386
    2011-12     1289
    2012-01     1589
    2012-02     1789
    2012-03     2192
    2012-04     2589
    2012-05     3325
    2012-06     3867
    2012-07     4582
    2012-08     4476
    2012-09     4035
    2012-10     3828
    2012-11     3706
    2012-12     3484
    2013-01     4418
    2013-02     4362
    2013-03     5421
    2013-04     5855
    2013-05     6721
    2013-06     6765
    2013-07     7950
    2013-08     8369
    2013-09     9125
    2013-10     7862
    2013-11     7751
    2013-12     8361
    2014-01    11111
    2014-02     9967
    2014-03    12058
    2014-04    12689
    2014-05    14895
    2014-06    15746
    2014-07    21696
    2014-08    21626
    2014-09    18774
    Name: id, dtype: int64



可见每年7，8，9月是用户新增最多的月份，猜测是夏季（北半球）旅游旺季。

## 2.渠道转化率分析


```python
#把渠道和推广方式用“-”连接起来。
all_users1['channel_provider'] = all_users1['affiliate_channel'].str.cat(all_users1['affiliate_provider'],sep ="_")

#访问量统计
visit = all_users1.groupby(['channel_provider'])['id'].count()

#注册量统计
booking = all_users1.groupby(['channel_provider'])['date_first_booking'].count()

#新建表用于合并计算列
v_b_channel = pd.merge(visit,booking,on = 'channel_provider')
v_b_channel.head()
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
      <th>id</th>
      <th>date_first_booking</th>
    </tr>
    <tr>
      <th>channel_provider</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>api_other</td>
      <td>8167</td>
      <td>2785</td>
    </tr>
    <tr>
      <td>content_facebook</td>
      <td>597</td>
      <td>68</td>
    </tr>
    <tr>
      <td>content_google</td>
      <td>3043</td>
      <td>451</td>
    </tr>
    <tr>
      <td>content_gsp</td>
      <td>455</td>
      <td>37</td>
    </tr>
    <tr>
      <td>content_other</td>
      <td>22</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 计算渠道转化率
v_b_channel['channel_rate'] = round(v_b_channel['date_first_booking']/v_b_channel['id'],2)
v_b_channel = v_b_channel.sort_values(by='channel_rate',ascending = False)
v_b_channel
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
      <th>id</th>
      <th>date_first_booking</th>
      <th>channel_rate</th>
    </tr>
    <tr>
      <th>channel_provider</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>sem-brand_baidu</td>
      <td>8</td>
      <td>5</td>
      <td>0.62</td>
    </tr>
    <tr>
      <td>direct_other</td>
      <td>301</td>
      <td>164</td>
      <td>0.54</td>
    </tr>
    <tr>
      <td>sem-non-brand_daum</td>
      <td>2</td>
      <td>1</td>
      <td>0.50</td>
    </tr>
    <tr>
      <td>seo_other</td>
      <td>329</td>
      <td>156</td>
      <td>0.47</td>
    </tr>
    <tr>
      <td>other_craigslist</td>
      <td>3475</td>
      <td>1616</td>
      <td>0.47</td>
    </tr>
    <tr>
      <td>sem-brand_yandex</td>
      <td>7</td>
      <td>3</td>
      <td>0.43</td>
    </tr>
    <tr>
      <td>sem-brand_naver</td>
      <td>7</td>
      <td>3</td>
      <td>0.43</td>
    </tr>
    <tr>
      <td>other_other</td>
      <td>4034</td>
      <td>1508</td>
      <td>0.37</td>
    </tr>
    <tr>
      <td>sem-non-brand_google</td>
      <td>18092</td>
      <td>6516</td>
      <td>0.36</td>
    </tr>
    <tr>
      <td>api_other</td>
      <td>8167</td>
      <td>2785</td>
      <td>0.34</td>
    </tr>
    <tr>
      <td>sem-non-brand_vast</td>
      <td>830</td>
      <td>271</td>
      <td>0.33</td>
    </tr>
    <tr>
      <td>direct_direct</td>
      <td>181270</td>
      <td>59234</td>
      <td>0.33</td>
    </tr>
    <tr>
      <td>sem-non-brand_bing</td>
      <td>916</td>
      <td>296</td>
      <td>0.32</td>
    </tr>
    <tr>
      <td>sem-non-brand_other</td>
      <td>144</td>
      <td>45</td>
      <td>0.31</td>
    </tr>
    <tr>
      <td>sem-brand_google</td>
      <td>34273</td>
      <td>10705</td>
      <td>0.31</td>
    </tr>
    <tr>
      <td>other_padmapper</td>
      <td>836</td>
      <td>252</td>
      <td>0.30</td>
    </tr>
    <tr>
      <td>seo_google</td>
      <td>9282</td>
      <td>2739</td>
      <td>0.30</td>
    </tr>
    <tr>
      <td>remarketing_google</td>
      <td>1266</td>
      <td>368</td>
      <td>0.29</td>
    </tr>
    <tr>
      <td>sem-non-brand_baidu</td>
      <td>18</td>
      <td>5</td>
      <td>0.28</td>
    </tr>
    <tr>
      <td>seo_yahoo</td>
      <td>652</td>
      <td>174</td>
      <td>0.27</td>
    </tr>
    <tr>
      <td>other_facebook-open-graph</td>
      <td>566</td>
      <td>141</td>
      <td>0.25</td>
    </tr>
    <tr>
      <td>sem-non-brand_naver</td>
      <td>59</td>
      <td>15</td>
      <td>0.25</td>
    </tr>
    <tr>
      <td>seo_bing</td>
      <td>699</td>
      <td>162</td>
      <td>0.23</td>
    </tr>
    <tr>
      <td>seo_facebook</td>
      <td>3394</td>
      <td>724</td>
      <td>0.21</td>
    </tr>
    <tr>
      <td>sem-brand_bing</td>
      <td>2104</td>
      <td>375</td>
      <td>0.18</td>
    </tr>
    <tr>
      <td>content_google</td>
      <td>3043</td>
      <td>451</td>
      <td>0.15</td>
    </tr>
    <tr>
      <td>other_email-marketing</td>
      <td>270</td>
      <td>37</td>
      <td>0.14</td>
    </tr>
    <tr>
      <td>other_meetup</td>
      <td>358</td>
      <td>46</td>
      <td>0.13</td>
    </tr>
    <tr>
      <td>sem-non-brand_yandex</td>
      <td>8</td>
      <td>1</td>
      <td>0.12</td>
    </tr>
    <tr>
      <td>content_facebook</td>
      <td>597</td>
      <td>68</td>
      <td>0.11</td>
    </tr>
    <tr>
      <td>content_other</td>
      <td>22</td>
      <td>2</td>
      <td>0.09</td>
    </tr>
    <tr>
      <td>content_gsp</td>
      <td>455</td>
      <td>37</td>
      <td>0.08</td>
    </tr>
    <tr>
      <td>sem-brand_other</td>
      <td>39</td>
      <td>3</td>
      <td>0.08</td>
    </tr>
    <tr>
      <td>sem-non-brand_yahoo</td>
      <td>1</td>
      <td>0</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>sem-brand_daum</td>
      <td>1</td>
      <td>0</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>seo_baidu</td>
      <td>6</td>
      <td>0</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>content_yandex</td>
      <td>1</td>
      <td>0</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>remarketing_yandex</td>
      <td>2</td>
      <td>0</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>other_wayn</td>
      <td>8</td>
      <td>0</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>sem-non-brand_facebook</td>
      <td>5</td>
      <td>0</td>
      <td>0.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 有些转化率高，因为用户样本数量少，所以样本选择中，选’id数量‘大于平均值的看看
v_b_channel.loc[v_b_channel['id'] > v_b_channel['id'].mean(),:].head(15)
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
      <th>id</th>
      <th>date_first_booking</th>
      <th>channel_rate</th>
    </tr>
    <tr>
      <th>channel_provider</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>sem-non-brand_google</td>
      <td>18092</td>
      <td>6516</td>
      <td>0.36</td>
    </tr>
    <tr>
      <td>api_other</td>
      <td>8167</td>
      <td>2785</td>
      <td>0.34</td>
    </tr>
    <tr>
      <td>direct_direct</td>
      <td>181270</td>
      <td>59234</td>
      <td>0.33</td>
    </tr>
    <tr>
      <td>sem-brand_google</td>
      <td>34273</td>
      <td>10705</td>
      <td>0.31</td>
    </tr>
    <tr>
      <td>seo_google</td>
      <td>9282</td>
      <td>2739</td>
      <td>0.30</td>
    </tr>
  </tbody>
</table>
</div>



airbnb的整体渠道转化率表现很好，多数渠道的转化率都在30%以上，其中：

<br/> * SEO: search engine optimization, SEM: search engine marketing,SEM is a broader term than SEO. Where SEO aims to provide better organic search results, SEM uses the search engines to advertise your webs.
<br/> * Some of the most common SEM best practices include: (1)Using keywords and keyword analysis;
(2) Search engine optimization (SEO);
(3) Building ads and content for local listings  and geo-targeted ads;
(4) Pay-per-click (PPC)  advertising campaigns.

<br/> API: An application program interface, is a set of routines, protocols, and tools for building software applications，应用程式介面。

<br/> 可见表现最好的为谷歌竞价（SEM）,其中品牌竞价注册量大于非品牌竞价的注册量。
<br/> 渠道注册量符合二八定律，前7个渠道（总共有40个渠道推广）的注册量已经占据了产品总的渠道来源的90%以上。

## 3.营销广告分析


```python
# 统计营销广告
visit  = all_users1.groupby(['first_affiliate_tracked'])['id'].count().reset_index()
booking = all_users1.groupby(['first_affiliate_tracked'])['date_first_booking'].count().reset_index()
```


```python
# 列合并形成新表
v_b_trac = pd.merge(visit,booking,on = 'first_affiliate_tracked')
v_b_trac
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
      <th>first_affiliate_tracked</th>
      <th>id</th>
      <th>date_first_booking</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>linked</td>
      <td>62064</td>
      <td>20102</td>
    </tr>
    <tr>
      <td>1</td>
      <td>local ops</td>
      <td>69</td>
      <td>9</td>
    </tr>
    <tr>
      <td>2</td>
      <td>marketing</td>
      <td>281</td>
      <td>63</td>
    </tr>
    <tr>
      <td>3</td>
      <td>omg</td>
      <td>54859</td>
      <td>16425</td>
    </tr>
    <tr>
      <td>4</td>
      <td>product</td>
      <td>2353</td>
      <td>542</td>
    </tr>
    <tr>
      <td>5</td>
      <td>tracked-other</td>
      <td>6655</td>
      <td>2290</td>
    </tr>
    <tr>
      <td>6</td>
      <td>untracked</td>
      <td>143181</td>
      <td>47739</td>
    </tr>
  </tbody>
</table>
</div>




```python
# rate = booking/visit,计算式中用原始字段
v_b_trac['rate'] = round(v_b_trac['date_first_booking']/v_b_trac['id'],2)
```


```python
# 重命名列名，按rate降序排列
v_b_trac.rename(columns={'first_affiliate_tracked':'first_affiliate_tracked','id':'visit',
                    'date_first_booking':'booking'})
v_b_trac = v_b_trac.sort_values(by='rate',ascending=False)
v_b_trac
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
      <th>first_affiliate_tracked</th>
      <th>id</th>
      <th>date_first_booking</th>
      <th>rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>5</td>
      <td>tracked-other</td>
      <td>6655</td>
      <td>2290</td>
      <td>0.34</td>
    </tr>
    <tr>
      <td>6</td>
      <td>untracked</td>
      <td>143181</td>
      <td>47739</td>
      <td>0.33</td>
    </tr>
    <tr>
      <td>0</td>
      <td>linked</td>
      <td>62064</td>
      <td>20102</td>
      <td>0.32</td>
    </tr>
    <tr>
      <td>3</td>
      <td>omg</td>
      <td>54859</td>
      <td>16425</td>
      <td>0.30</td>
    </tr>
    <tr>
      <td>4</td>
      <td>product</td>
      <td>2353</td>
      <td>542</td>
      <td>0.23</td>
    </tr>
    <tr>
      <td>2</td>
      <td>marketing</td>
      <td>281</td>
      <td>63</td>
      <td>0.22</td>
    </tr>
    <tr>
      <td>1</td>
      <td>local ops</td>
      <td>69</td>
      <td>9</td>
      <td>0.13</td>
    </tr>
  </tbody>
</table>
</div>



# 转化漏斗分析

因数据包太大，Jupyter Notebook无法加载，该部分转由MySQL分析。
* the amount of different types of action: 360
* the amount of different types of action_type: 11
* the amount of different types of action_detail: 156


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
create table funnel 
(
event VARCHAR (20) primary KEY, user_amount INT (10)
);

insert into funnel values ('Acquisition',135484),
						  ('Activation',114001),
						  ('Register',73815),
						  ('Booking',10367),
						  ('Checkout',9019),
						  ('Repurchase',5446);
												
```


*Reference:*
<br>[https://growthrocks.com/blog/aarrr-framework/](https://growthrocks.com/blog/aarrr-framework/)
<br>[https://github.com/emindeniz/FunnelAnalysis](https://github.com/emindeniz/FunnelAnalysis/blob/master/Funnel_Analysis.ipynb)
<br>[https://medium.com/@henryfeng/customer-funnel-analysis-for-online-retailer](https://medium.com/@henryfeng/customer-funnel-analysis-for-online-retailer-using-pivot-table-and-clustering-in-python-bdcc88824d0b)
<br>[https://36kr.com/p/5157285](https://36kr.com/p/5157285)
<br>[https://blog.csdn.net/](https://blog.csdn.net/weixin_42334748/article/details/102567323?ops_request_misc=%7B%22request%5Fid%22%3A%22158324033919725256701111%22%2C%22scm%22%3A%2220140713.130056874..%22%7D&request_id=158324033919725256701111&biz_id=0&utm_source=distribute.pc_search_result.none-task)
<br>[https://www.tableau.com](https://www.tableau.com/about/blog/2018/6/three-different-ways-build-funnels-tableau-and-why-89871)
<br>[https://fivetran.com/blog/funnel-analysis](https://fivetran.com/blog/funnel-analysis)
