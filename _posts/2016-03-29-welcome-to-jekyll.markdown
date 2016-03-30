---
layout: post
title:  "《艾家网》IOS端项目总结"
date:   2016-03-29 22:01:46 +0800
categories: jekyll update
---

《艾家网》是一个外包项目，做了差不多两个月，总体来说做的还是比较认真的。下面从几个方面去对这个项目做一个总结。
  
## 1.目录结构

艾家网的目录结构如下：
	
    ├─ AppDelegate
    ├─ ViewControllers
    ├─ Sections			
    ├─ Managers
    ├─ APIRequests
    ├─ Models
    ├─ General
    ├─ Stores
    ├─ Helpers
    ├─ Macros
    ├─ Config
    ├─ Vendors
    ├─ Resources
    
这种分类，我把它称为按 “角色” 分类，因为我是在是找不出更贴切的词语来描述这种分类方式。比如xxxViewController 它的角色为ViewControllers.  AEGPageFlowManager 角色为 Manager。

* #### AppDelegate  
该目录存放的是 AppDelegate.h(.m) 和 文件，是整个app的入口文件，所以单独拿出来。还有AppDelegate+VendorAccessory.h(.m) 这个文件放的是一些需要在入口添加的辅助设置，比如：setUpYTKNetwork ，setUpUMengSocial。

* #### ViewControllers
改目录存放一些ViewController, 这些都是业务类（client），文件夹下面的文件细分是业务页面模块，当然也包括几个通用的controller： AEGBaseViewController， AEGBaseNavigationController， AEGLaunchViewController，AEGGuideViewController，AEGMainViewController。 

* ####  Sections
放置一些app的具体单元，如confirmBar, segmentControl, selectItemBar 还有各种的tableViewElement(包括 cells，header) ，CollectionViewElement。

* ####  Managers
管理者，一般是单例。如 AEGPageFlowManager 负责页面流程管理工作。（注：但是并不是所有的都可以作为单例的manager 可以参考 [避免滥用单例](http://objccn.io/issue-13-2/)。

* ####  APIRequests
整个工程中，网络接口用的是[YTKNetwork](https://github.com/yuantiku/YTKNetwork)。YTKNetwork是猿题库 iOS 研发团队基于 AFNetworking 封装的 iOS 网络库，其实现了一套 High Level 的 API，提供了更高层次的网络访问抽象。基本的思想是把每一个网络请求封装成对象。所以使用 YTKNetwork，你的每一个请求都需要继承YTKRequest类，通过覆盖父类的一些方法来构造指定的网络请求。使用了Command 模式。 这个文件存放各种request，由于接口参数需要做加密签名，而且get和post的签名方式不一样，我把这些共性的东西抽了出来做了一个 AEGRequest ，所有具体的request都是继承自 AEGRequest。

* ####  Models
存放 models，分为3种：JsonModel, coreDataModel, CustomModel. JsonModel代表着 request 返回的json，利用MJExtension 来实现ORM。 model文件用插件 [ESJSonFormat](https://github.com/EnjoySR/ESJsonFormat-Xcode) 来生成。这样就节省了很多工作，但是有一点要修改，就是基本类型如int我比较偏向于用NSNumber来表示，所以要改，有空可以改一下源码。coreDataModel 是coreData 用到的model。

* ####  General
General 顾名思义，一般的，通用的，所以在这个文件中会放一些通用的模块和架构层的模块如 TOWebViewController，通用的webViewController, DDPopupView, JHTableViewAdapter, LGHCollectionViewAdapter. 还有category JHTableViewController+MJRefresh， UIViewController+MBProgressHUD 这些同样适用于其它工程的公有的部分。

* ####  Stores
这个文件现在只存了一个AEGAccountStorage。这是一个Account（账户），它有一个AEGUserProfile的属性，这个类相当于userDetail.其实Account 与UserProfile的关系相当于User与userDetail的关系，为了更加贴切的表示和区分这两者的功能我把名字改了，AEGAccountStorage 是一个帐户，他有一个个人简历AEGUserProfile属性。但是这个账号AEGAccountStorage通过- (instancetype)initWithAccountId:(NSNumber *)accountId 初始化，通过- (BOOL)saveUserProfile:(AEGUserProfile *)userProfile来保存UserProfile 到手机，这样下次再没有网络的启动下也能拿到用户信息UserProfile。

* ####  Helpers
帮助类，每个文件是相应的泪方法 如AEGFileHelper负责文件操作， AEGFormatVerifyHelper 负责手机，邮箱等的格式验证。

* ####  Macros


* ####  Config

* ####  Vendors

* ####  Resources


{% highlight objc %}
NSAttributedString *attributeString2 = [[NSAttributedString alloc] initWithString:[NSString stringWithFormat:@"￥%@", orderDetail.Voucher] attributes:@{NSFontAttributeName: UIFontWithSize(kFontSize02), NSForegroundColorAttributeName:UIColorFromHex(kColor01)}];
        [mutableAttributeStr appendAttributedString:attributeString2];
        
        depositInfoCellModel.voucherAttributeString = mutableAttributeStr;
        depositInfoCellModel.refundMessage = orderDetail.RefundMessage;
        [depositSectionModel.cellModels addObject:depositInfoCellModel];
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
