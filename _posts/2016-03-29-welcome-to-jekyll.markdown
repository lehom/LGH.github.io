---
layout: post
title:  "《艾家网》IOS端项目总结"
date:   2016-03-29 22:01:46 +0800
categories: jekyll update
---

《艾家网》是一个外包项目，做了差不多两个月，总体来说做的还是比较认真的。下面从几个方面去对这个项目做一个总结。
  
###项目目录结构
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

* ####AppDelegate
这个目录存放的是 AppDelegate.h(.m) 和 文件，是整个app的入口文件，所以单独拿出来。还有AppDelegate+VendorAccessory.h(.m) 这个文件放的是一些需要在入口添加的辅助设置，比如：setUpYTKNetwork ，setUpUMengSocial。
* ####ViewControllers
这个目录存放

Jekyll also offers powerful support for code snippets:

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
