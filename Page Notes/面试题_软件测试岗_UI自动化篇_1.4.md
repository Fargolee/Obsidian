---
page-title: "面试题_软件测试岗_UI自动化篇_1.4"
url: https://mp.weixin.qq.com/s/_EMJ6wr6O4izlh2uobBKUQ
date: "2024-04-08 18:18:03"
---
![图片](https://mmbiz.qpic.cn/mmbiz_png/434uGiasvPDzAJWTTLkjvm88F9IUW0EL8Gpt4Lic44PmbLJ4ucrF2Bm3icTvueBza7rcx7CedCRJpcibyZic1JFd9JA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

软件测试UI自动化是现代软件开发中不可或缺的一环。随着软件开发速度的加快和市场的竞争日益激烈，确保软件质量和提供优质用户体验变得至关重要。手动测试虽然在过去是常见的测试方法，但在大型和复杂的应用程序中，它变得耗时且容易出错。软件测试UI自动化的出现解决了这些挑战。

软件测试UI自动化通过使用自动化工具和脚本来模拟用户交互、执行测试用例和检测界面问题。它能够帮助测试团队提高测试效率和准确性，减少人工测试的工作量，并提供一致性的测试结果。自动化测试可以快速执行大量的测试用例，覆盖广泛的功能和场景，从而更早地发现和修复软件中的缺陷。

另外，软件测试UI自动化还具有可重复性和可维护性的优势。一旦编写了自动化测试脚本，它们可以反复执行，确保每次执行的结果一致。这样可以确保软件在不同环境和配置下的一致性表现。此外，当应用程序发生变化时，只需更新相关的自动化脚本，而不需要重新执行整个测试过程，大大节省了时间和精力。

通过软件测试UI自动化，测试团队还可以更早地介入软件开发过程，并与开发团队紧密合作。自动化测试可以帮助发现问题并及早解决，从而减少了软件开发周期中的延误和成本。

总的来说，软件测试UI自动化是提高测试效率、准确性和软件质量的关键步骤。它帮助团队更好地控制和管理软件质量，减少错误和缺陷的出现，并提供良好的用户体验。随着软件开发行业的不断发展，软件测试UI自动化的重要性将继续增长，并成为软件开发过程中的核心环节。

**01/什么是POM，为什么要使用它？**

POM是Page Object Model的简称，它是一种设计思想，而不是框架。大概的意思是，把一个一个页面，当做一个对象，页面的元素和元素之间操作方法就是页面对象的属性和行为，所以自然而然就用了类的思想来组织我们的页面。一般一个页面写一个类文件，这个类文件包含该页面的元素定位和业务操作方法

**02/如果页面元素经常发生需求变化，你是如何做?**

采用POM思想。好处就是只要改一个页面，我就去修改这个页面对象的元素定位和相关方法，脚本不需要修改。

**03/在你做自动化过程中，遇到了什么问题吗？举例下?**

1.频繁地变更UI，经常要修改页面对象里面代码

2.运行用例报错和处理，例如元素不可见，元素找不到这样异常

3.测试脚本复用，尽可能多代码复用

4.一些新框架产生的页面元素定位问题，例如ck编辑器，动态表格等

**04/举例一下你遇到过那些异常，在selenium自动化测试过程中**

```
ElementNotSelectableException ：元素不能选择异常
```

****05/如何处理alert弹窗****

```
我们常见的alert弹窗有两种：基于windows弹窗和基于web页面弹窗
```

********06/在selenium中如何处理多窗口？********

这个多窗口之间跳转处理，在实际selenium自动化测试经常遇到。就是，你点击一个链接，这个链接会在一个新的tab打开，然后你接下来要查找元素在新tab打开的页面，所以这里需要用到swithTo方法;需要获取当前浏览器多窗口句柄，然后根据判断跳转新句柄还是旧句柄

**07/你查找元素遇到过在Frame里面吗?你是如何处理Frame里面元素定位的？**

有时候我们知道元素定位表达式没有问题，但是还是提示no such element，那么我们就需要考虑这个元素是否在frame中。如果在，我们就需要从topwindow，通过swithcTo.Frame()方法来切换到目标frame中，可以通过frame的name、id和index三种方法来定位frame。

**08/如何处理下拉菜单？**

```
通常我们也可以通过Click方法来点击下拉菜单里面的元素，还有一种方法，在Selenium中有一个类叫Select，支持这种下拉菜单交互的操作。
```

留个问题，你有什么建议和想法，可以帮助团队提高UI自动化测试的效率和质量？

这些问题涵盖了软件测试UI自动化的关键概念、工具和技术的理解，以及在实践中遇到的挑战和解决方案。准备这些问题的答案将帮助你在面试中展示你对UI自动化测试的理解和经验，以及你的解决问题的能力和团队合作技巧。

以上为部分测试面试题，后续更多精彩试题，请关注订阅号第一时间进行查看，针对求职注意事项请查看文章：[金三银四，浅谈软件测试岗求职注意事项!](http://mp.weixin.qq.com/s?__biz=MzUyNTUwNTU5Nw==&mid=2247495202&idx=1&sn=8f525aad4d2521a219cb724a76f990fb&chksm=fa1fab70cd682266ff13776db192c797c980d9c973830fa52ee504450bff8eedd45374cc50a5&scene=21#wechat_redirect)  

针对面试题的巩固以及覆盖推荐：[《测试开发面试宝典》重磅推荐!](http://mp.weixin.qq.com/s?__biz=MzUyNTUwNTU5Nw==&mid=2247495190&idx=1&sn=a631bfbb113d5b08f04a07707eb1e43c&chksm=fa1fab44cd682252e634c5231e835ddee36328b270b2f3b20350717cae9f3197fcb08e36e4a1&scene=21#wechat_redirect)  

一个字：刷；热门面试题往死里刷，面试造火箭入职拧螺丝，NB吹到位梳理入职就成功，面试题全集给大家推荐我昨天的一篇文章里推荐的【测试开发面试宝典】[《测试开发面试宝典》重磅推荐!](http://mp.weixin.qq.com/s?__biz=MzUyNTUwNTU5Nw==&mid=2247495190&idx=1&sn=a631bfbb113d5b08f04a07707eb1e43c&chksm=fa1fab44cd682252e634c5231e835ddee36328b270b2f3b20350717cae9f3197fcb08e36e4a1&scene=21#wechat_redirect)  大家可以点开详情看看，真的很全，真心很值！

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

部分购买用户反馈，有部分同学购买后进行学习已经上岸大厂测开、国企测试岗位，拿到年薪30w+测开offer

**![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)**

目前限时特惠粉丝福利价格是79.9元，随着内容的不断升级迭代，价格还会不断上涨, 直接识别图片二维码即可下单!

1.  提前下载好blibli
    
2.  识别二维码  
    

3\. 使用默认浏览器打开跳转到blibli下载购买即可

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

祝各位大佬早日上岸!

**面试题精彩集锦，喜欢的朋友留关注不同错过**

[面试题\_软件测试岗位\_1.0](http://mp.weixin.qq.com/s?__biz=MzUyNTUwNTU5Nw==&mid=2247495313&idx=1&sn=a2ec431d5def2e29a855fbf891c8598a&chksm=fa1fabc3cd6822d5e1cd1cdb9393021d2114ff15de5d117229f9c407def1ba1cc97946c51bd3&scene=21#wechat_redirect)  

[面试题\_软件测试岗位\_1.1](http://mp.weixin.qq.com/s?__biz=MzUyNTUwNTU5Nw==&mid=2247495323&idx=1&sn=cb9dd2d7041d59d7ec2fa96e74421d61&chksm=fa1fabc9cd6822dfa9917029e3920810f07c8f7338c26b92bd461f0ac7e8092d89724b5f3da0&scene=21#wechat_redirect)  

[面试题\_软件测试常见Python编程思维题\_1.2](http://mp.weixin.qq.com/s?__biz=MzUyNTUwNTU5Nw==&mid=2247495335&idx=1&sn=45ed6da341ee75d27d63c10de630182f&chksm=fa1fabf5cd6822e376d2f985dc5a3e94704f49dbb6068a47b2bf4de971c2a3e6ce7b96944419&scene=21#wechat_redirect)

[面试题\_软件测试岗\_自动化篇\_1.3](http://mp.weixin.qq.com/s?__biz=MzUyNTUwNTU5Nw==&mid=2247495345&idx=1&sn=c621cf065b26410e0ee9073f046fdd58&chksm=fa1fabe3cd6822f578ae5cab434a6b2553f80e10932f02bfc145ae9e8fe7e576d2fdc01d50ea&scene=21#wechat_redirect)  

如果觉得有用，就请关注、点赞、在看、分享到朋友圈吧！