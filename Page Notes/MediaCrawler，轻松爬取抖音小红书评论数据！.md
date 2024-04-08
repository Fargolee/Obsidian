---
page-title: "MediaCrawler，轻松爬取抖音小红书评论数据！"
url: https://mp.weixin.qq.com/s/-lPmniYvJl56fLZZei3y_Q
date: "2024-04-08 19:27:53"
---
*![图片](https://mmbiz.qpic.cn/mmbiz_gif/y0SBuxfLhakRBx9pRgU2ibpXa3CWxVTFpNaa5TwKdYjSL6AMJ9gKaagibNRQbk4a0EFng11dVeHibvp0LugZ3eaAA/640?wx_fmt=gif&tp=webp&wxfrom=5&wx_lazy=1)*

大家好，我是小F～

今天给大家介绍一个**Python爬虫实战的项目**，MediaCrawler。

可以实现小红书爬虫，抖音爬虫， 快手爬虫， B站爬虫， 微博爬虫。

目前能抓取小红书、抖音、快手、B站、微博的视频、图片、评论、点赞、转发等信息。

![图片](https://mmbiz.qpic.cn/mmbiz_png/y0SBuxfLhakiatE5U89vDibJzU4dFAtpAHjwgzMzwlsOZ5c3mOiblhKcbszXSXOum7do5mGwfw3scfz8DHomHiaI9A/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

项目地址：  

*https://github.com/NanmiCoder/MediaCrawler*

原理：利用playwright搭桥，保留登录成功后的上下文浏览器环境，通过执行JS表达式获取一些加密参数 通过使用此方式，免去了复现核心加密JS代码，逆向难度大大降低。

下面小F就来介绍下如何使用~  

首先使用conda创建虚拟环境，Python版本3.9。

激活环境后，安装相关的依赖。  

# 创建conda环境  
conda create --name MediaCrawler python=3.9

# 激活环境  
conda activate MediaCrawler

# 安装相关依赖  
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple

# 安装playwright浏览器驱动  
playwright install

其中Playwright是微软推出来的一款自动化测试工具，是专门为满足端到端测试需求而创建的。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

最后还需要安装nodejs，版本为v16.20.2，要不然运行会报错。  

数据保存有三种方式，数据库、CSV、JSON。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

数据库地址可以在db\_config.py文件里配置。

支持redis、mysql、sqlite3。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

整个项目代码开源，项目代码结构如下。  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

一些常见的问题，大家可以看看。  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

环境搭建好以后，就可以执行代码啦~

# 从配置文件中读取关键词搜索相关的帖子并爬去帖子信息与评论  
python main.py --platform xhs --lt qrcode --type search

# 从配置文件中读取指定的帖子ID列表获取指定帖子的信息与评论信息  
python main.py --platform xhs --lt qrcode --type detail

# 其他平台爬虫使用示例, 执行下面的命令查看  
python main.py --help

具体的配置可以去base\_config.py文件里修改。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

这里以小红书作为例子，来实验一下。

命令行运行代码，结果如下。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

成功保存了csv数据，包含帖子及评论信息。  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

下一步就是对数据进行分析处理了，大家可以自行去学习使用。

项目源码，公众号后台回复：「**MediaCrawler**」，即可获得。

爬取这些平台（小红书、抖音、快手、B站、微博）的笔记、视频评论和帖子评论可以为多个领域创造价值。下面举几个例子说明：

**① 市场研究和消费者洞察**

通过分析这些数据，企业可以获得有关消费者偏好、兴趣、反馈和行为趋势的深入洞察。这为产品开发、市场定位和优化营销策略提供了数据支持。

**② 品牌舆情监控**  

企业可以实时监控和分析公众对其品牌、产品或服务的看法和情绪变化。这有助于快速响应可能的负面舆论，维护品牌形象。

**③ 竞争对手分析**

通过比较分析竞争对手在上述平台的表现，企业可以了解竞争对手的市场策略、客户反馈以及优缺点，从而调整自己的策略以保持竞争优势。

**④ 内容策略优化**

了解哪些主题或视频类型最受欢迎，可以帮助内容创造者、营销人员和媒体公司制定更符合用户需求和喜好的内容策略。

**⑤ 社交媒体趋势分析**

分析评论数据可以揭示当前的社交媒体趋势、热议话题和病毒内容，为内容创新提供灵感。

**⑥ 顾客服务和产品反馈**

直接从用户评论中提取问题和反馈，可以让企业迅速改进产品和服务，提升顾客满意度。  

注：使用这些数据时，要特别注意遵守相关法律法规（如数据保护法），尊重用户隐私，确保数据的合法、合规获取和使用。不当的数据使用不仅可能违反法律，还可能对企业声誉和用户信任造成伤害。

****万水千山总是情，点个 👍 行不行**。**

**推荐阅读**

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzU4OTYzNjE2OQ==&mid=2247484115&idx=1&sn=447d90d9e9d17b963c6dc76f7d691735&chksm=fdcb35f5cabcbce3bb4318fa7271a367a2beca95e6aaa02670a61844c6497b6aa2a258588b90&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzU4OTYzNjE2OQ==&mid=2247484095&idx=1&sn=a284ba324550829c969fa2cda0da723c&chksm=fdcb3599cabcbc8f96df521eb5ce50910da152de627e47a69b26e9f2da5920dc6afe4ad2642f&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzU4OTYzNjE2OQ==&mid=2247484076&idx=1&sn=fac8b75e2fbdb8eecff16b1faa4dc7f2&chksm=fdcb358acabcbc9c20769d3800f77f7cafb16844486e2c3fd35b0d567923eeac352189cc6285&scene=21#wechat_redirect)

**···  END  ···**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)