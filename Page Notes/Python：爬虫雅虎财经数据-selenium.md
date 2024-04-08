---
page-title: "Python：爬虫雅虎财经数据-selenium"
url: https://www.lianxh.cn/details/1306.html
date: "2024-04-08 14:33:52"
---
> **作者**：陈卓然 (中山大学)  
> **邮箱**：[chenzhr25@mail2.sysu.edu.cn](mailto:chenzhr25@mail2.sysu.edu.cn)

> **编者按**：本文参考自 Bryan Pfalzgraf 的 [How to Use Selenium to Web-Scrape with Example](https://towardsdatascience.com/how-to-use-selenium-to-web-scrape-with-example-80f9b23a843a)，以及连享会课程 [文本分析-爬虫-机器学习](https://www.lianxh.cn/news/88426b2faeea8.html)，特此致谢！

-   **Title**: Python：爬虫雅虎财经数据-selenium
-   **Keywords**: 爬取, 股票指数, 静态网页

本推文将以爬取世界主要股票指数为例，简要介绍 Python 爬虫的方法。

## 1\. Selenium

现在，很多网页通过使用 JavaScript 的 Ajax 技术实现了网页内容的动态改变。在碰到动态页面时，一种方法是精通JavaScript，并使用浏览器跟踪浏览器行为，分析 JavaScript 脚本，进而使用以上的方法模拟浏览器请求。但是这种方法非常复杂，很多时候 JavaScript 可能会复杂到一定程度，使得分析异常困难。

另外一种方法是使用 Selenium 直接调用浏览器，浏览器自动执行 JavaScript，然后调用浏览器的 HTML 即可。这种方法非常方便，但是速度异常之慢。

为了实现这一方法，我们首先要安装 `selenium`：`pip install selenium`。`selenium` 是 Python 中用来自动调用浏览器的一个包，在从网页中爬取数据的过程中可以不需要我们自己去寻找真正的网页源代码。

`selenium` 中一个重要的类是 `webdriver`，它能够自动化地打开一个网页，帮助我们自动化进行浏览网页。`webdriver` 支持 Google Chrome，Internet Explorer，Firefox，Safari 和 Opera。

这里以一个爬取 NBA 球员薪酬网站为例，简要说明 selenium 的使用方法。首先我们需要定义一个 driver 的变量，用来爬取数据的引擎。

```
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import pandas as pd
driver = webdriver.Chrome()
```

然后我们需要使用 Python 去打开一个我们想要爬取的网站。

```
driver.get('https://hoopshype.com/salaries/players/')
```

接下来我们需要定位爬取信息的位置，为了提取需要的信息，我们需要定位到这个信息元素的 XPath。XPath 是一个用来寻找一个网页中任何元素的语法，为了找到 XPath, 我们需要右击鼠标，然后选择 `检查(inspect)`。

![](https://fig-lianxh.oss-cn-shenzhen.aliyuncs.com/Python%E7%88%AC%E8%99%AB%E4%BB%A5%E9%9B%85%E8%99%8E%E8%B4%A2%E7%BB%8F%E4%B8%BA%E4%BE%8B_%E9%99%88%E5%8D%93%E7%84%B6_Fig01.png)

我们可以看到 `Stephen Curry` 的 HTML 代码是：

```
<td class=”name”>
<a href=”https://hoopshype.com/player/stephen-curry/salary/">
Stephen Curry </a>
</td>
```

在将其转换成 XPath 之前，让我们再检查一下另外一个明星 Russell Westbrook：

```
<td class=”name”>
<a href=”https://hoopshype.com/player/russell-westbrook/salary/">
>Russell Westbrook </a>
</td>
```

可以看到两者的相似之处在于 `<td class=”name”>`，也就是说我们可以据此来得到所有明星的名字。我们将其转换为 XPath: `//td[@class=”name”]`。所有的 XPath 以两条 `//` 开始，然后我们需要 `td` 标签，以及 `td` 标签下的 `name` 类。

```
from selenium.webdriver.common.by import By
```

```
driver = webdriver.Chrome()
driver.get('https://hoopshype.com/salaries/players/')
players = driver.find_elements(By.XPATH, '//td[@class="name"]')
players_list = []
for p in range(len(players)):
    players_list.append(players[p].text)
```

通过相同的办法，我们也可以找到这些球星的薪水。

```
salaries_list = []
for item in salaries:
    salaries_list.append(item.text)
```

```
df = pd.DataFrame(list(zip(players_list, salaries_list)))
```

player

salary

1

Stephen Curry

$51,915,615

2

Kevin Durant

$47,649,433

3

Nikola Jokic

$47,607,350

4

LeBron James

$47,607,350

5

Joel Embiid

$47,607,350

6

Bradley Beal

$46,741,590

7

Paul George

$45,640,084

8

Kawhi Leonard

$45,640,084

9

Giannis Antetokounmpo

$45,640,084

10

Damian Lillard

$45,640,084

11

Jimmy Butler

$45,183,960

12

Klay Thompson

$43,219,440

13

Rudy Gobert

$41,000,000

14

Fred VanVleet

$40,806,300

15

Anthony Davis

$40,600,080

16

Trae Young

$40,064,220

17

Zach LaVine

$40,064,220

18

Luka Doncic

$40,064,220

19

Tobias Harris

$39,270,150

20

Ben Simmons

$37,893,408

21

Pascal Siakam

$37,893,408

22

Kyrie Irving

$37,037,037

23

Jrue Holiday

$36,861,707

...

...

...

507

Micah Potter

$559,782

508

Eugene Omoruyi

$559,782

509

Malik Fitts

$555,217

510

Didi Louzada

$268,032

## 2\. 爬取雅虎财经数据

在了解如何使用 Selenium 之后，我们来爬取 Yahoo Finance 中的 [世界主要股票指数](https://finance.yahoo.com/world-indices/)。这次我们选择的浏览器是微软的 Edge 浏览器：

```
driver2 = webdriver.Edge()
```

这次采取和前文爬取 NBA 明星薪酬数据不太相同的方法，我们引入了 `BeautifulSoup` 包，将网页的 HTML 爬取下来。

```
driver2.get("https://finance.yahoo.com/world-indices/")
html2 = driver2.execute_script('return document.body.innerHTML;')
soup2 = BeautifulSoup(html2,'lxml')
```

接下来，我们按照前文的办法寻找对应的标签，以及标签下面的类，分别获得指数简称，指数全称，实时价格，价格数值变化，价格的百分比变化，以及成交量.

```
indices = [entry.text for entry in \
    soup2.find_all("a", {"class":"Fw(600) C($linkColor)"})]
names = [item.text for item in \
    soup2.find_all("td", {"class":"Va(m) Ta(start) Px(10px) Fz(s)","aria-label":"Name"})]
lastprice = [entry.text for entry in \
    soup2.find_all("fin-streamer", {"data-test":"colorChange", "data-field":"regularMarketPrice"})]
change = [entry.text for entry in \
    soup2.find_all("td", {"class":"Va(m) Ta(end) Pstart(20px) Fw(600) Fz(s)", "aria-label":"Change"})]
perc_change = [entry.text for entry in \
    soup2.find_all("td", {"class":"Va(m) Ta(end) Pstart(20px) Fw(600) Fz(s)", "aria-label":"% Change"})]
volumne = [item.text for item in \
    soup2.find_all("td", {"class":"Va(m) Ta(end) Pstart(20px) Fz(s)", "aria-label":"Volume"})]
df2 = pd.DataFrame((list(zip(indices, names, lastprice, change, perc_change, volumne))), \
    columns=["indices", "names", "lastprice", "change", "perc_change", "volume"])
```

indices

names

lastprice

change

perc\_change

volume

0

^GSPC

S&P 500

4,582.23

44.82

+0.99%

2.36B

1

^DJI

Dow Jones Industrial Average

35,459.29

176.57

+0.50%

369.001M

2

^IXIC

NASDAQ Composite

14,316.66

266.55

+1.90%

3.955B

3

^NYA

NYSE COMPOSITE (DJ)

16,363.26

92.66

+0.57%

0

4

^XAX

NYSE AMEX COMPOSITE INDEX

4,354.70

88.38

+2.07%

0

5

^BUK100P

Cboe UK 100

767.75

\-0.38

\-0.05%

0

6

^RUT

Russell 2000

1,981.54

26.64

+1.36%

0

7

^VIX

CBOE Volatility Index

13.33

\-1.08

\-7.49%

0

8

^FTSE

FTSE 100

7,694.27

1.51

+0.02%

0

9

^GDAXI

DAX PERFORMANCE-INDEX

16,469.75

63.72

+0.39%

0

10

^FCHI

CAC 40

7,476.47

11.23

+0.15%

0

11

^STOXX50E

ESTX 50 PR.EUR

4,466.50

19.06

+0.43%

0

12

^N100

Euronext 100 Index

1,400.61

\-0.87

\-0.06%

0

13

^BFX

BEL 20

3,788.39

\-14.26

\-0.38%

0

14

IMOEX.ME

MOEX Russia Index

2,222.51

\-4.14

\-0.19%

0

15

^N225

Nikkei 225

32,759.23

\-131.93

\-0.40%

0

16

^HSI

HANG SENG INDEX

19,916.56

277.45

+1.41%

0

17

000001.SS

SSE Composite Index

3,275.93

59.25

+1.84%

2.452B

18

399001.SZ

Shenzhen Index

11,100.40

176.62

+1.62%

1.819B

19

^STI

STI Index

3,371.17

33.75

+1.01%

0

20

^AXJO

S&P/ASX 200

7,403.60

\-52.3

\-0.70%

0

21

^AORD

ALL ORDINARIES

7,616.10

\-56.5

\-0.74%

0

22

^BSESN

S&P BSE SENSEX

66,160.20

\-106.62

\-0.16%

0

...

...

...

...

32

^MERV

MERVAL

38,390.84

233.89

+0.61%

0

33

^TA125.TA

TA-125

1,888.39

26.54

+1.43%

0

34

^CASE30

EGX 30 Price Return Index

17,348.10

\-48.1

\-0.28%

1.74M

35

^JN0U.JO

Top 40 USD Net TRI Index

4,458.29

36.8

+0.83%

0

## 3\. 小结

本推文简要介绍了 Selenium 爬取简单的静态网页的方法。事实上，Selenium 能够做的远不止于此，它还可以用来爬取动态网页等等，感兴趣的读者可以进一步深入了解 [Selenium 的有关知识](https://www.selenium.dev/documentation/webdriver/)。

## 4\. 相关推文

> Note：产生如下推文列表的 Stata 命令为：  
>   `lianxh 爬虫, m`  
> 安装最新版 `lianxh` 命令：  
>   `ssc install lianxh, replace`

-   专题：[文本分析-爬虫](https://www.lianxh.cn/blogs/36.html)
    -   [Stata爬虫：爬取地区宏观数据](https://www.lianxh.cn/news/815b934b27073.html)
    -   [Stata爬虫：爬取Ａ股公司基本信息](https://www.lianxh.cn/news/9c1607842eb49.html)
    -   [Stata爬虫-正则表达式：爬取必胜客](https://www.lianxh.cn/news/8c6be3c47d2eb.html)
    -   [Python爬虫: 《经济研究》研究热点和主题分析](https://www.lianxh.cn/news/2fb619662956e.html)
-   专题：[Python-R-Matlab](https://www.lianxh.cn/blogs/37.html)
    -   [Python：多进程、多线程及其爬虫应用](https://www.lianxh.cn/news/8c175c980bcd9.html)
    -   [Python爬虫1：小白系列之requests和json](https://www.lianxh.cn/news/b4f20b9c35e27.html)
    -   [Python爬虫2：小白系列之requests和lxml](https://www.lianxh.cn/news/22c7f1ab6295e.html)
    -   [Python爬虫：爬取华尔街日报的全部历史文章并翻译](https://www.lianxh.cn/news/e080bab8798f9.html)
    -   [Python爬虫：从SEC-EDGAR爬取股东治理数据-Shareholder-Activism](https://www.lianxh.cn/news/f2ec917e39a6c.html)