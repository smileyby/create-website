创建网站遇到的那些坑
=================

作为一个技术开发，拥有一个自己的博客网站还是蛮不错的。所以就想着自己弄一个网站来发表一些自己在平时遇到的一些技术问题。

不做不知道，这里面的坑还真不少。

就拿域名备案这个事情来说吧，我今天申请了三次都被拒绝了。这个信息填的我内心很崩溃啊。

等我把自己的网站建起来，在把这个过程中遇到的坑总结一下写在这里。

本人是在阿里云申请的域名，下面所有的配置都是基于阿里云来配置的。

## 域名申请

我是在阿里云的 [万网](https://wanwang.aliyun.com/) 购买的域名，买个几块钱一年的就好。（如果你是想注册一些域名来出售的话就另当别论了）

* 购买域名
* 购买虚拟主机或服务器
* 域名解析到虚拟主机或服务器
* 申请域名备案
* 阿里云和所在地通信管理局对域名备案进行审核
* 审核通过，开始进行站点配置

这里主要说一下，阿里云域名备案的审核流程和需要提交的申请材料：

1. 初次申请可下载阿里云app在app中提交审核相关资料（包括身份证正反面清晰图，个人网站备案承诺书）
2. 提交后阿里云会在1-2个工作日内，以电话方式联系确认网站信息（如实回答即可）
3. 初审通过后，阿里云会让你提交（网站信息真实性核验单）
4. 再次提交审核通过后，需要购买阿里云指定的幕布---拍摄网站管理者半身照（按照阿里云规定拍摄即可，我是自拍搞定的。）
4. 再次提交后审核通过则直接提交至所在地通信管理局进行审核（这个过程至少需要一周时间，快的话当日即可审核通过）

上面所有提到**个人网站备案承诺书** **网站信息真实性核验单** 需自行打印并按照阿里云提供的规范进行填写。

## 配置网站https

我是用阿里云的虚拟主机，通过配置站点的CDN来实现网站域名https。（但这种方式会被chrome firefox opera等浏览器标记为不安全）。

具体的配置方法如下：

> 1.申请阿里云https免费安全证书

> ![云盾证书服务](http://oqpmmru7y.bkt.clouddn.com/1zhengshu.png)
> ![购买证书](http://oqpmmru7y.bkt.clouddn.com/2maizhengshu.png)
> ![选择证书类型](http://oqpmmru7y.bkt.clouddn.com/3xuanzezhengshu.png)
> ![查看证书签发状态](http://oqpmmru7y.bkt.clouddn.com/4qianfazhengshu.png)

> 2.在阿里云的CDN服务中新建加速域名

> ![](http://oqpmmru7y.bkt.clouddn.com/5tianjiayuming.png)
> ![](http://oqpmmru7y.bkt.clouddn.com/6tianjiayumingcdn.png)
> ![](http://oqpmmru7y.bkt.clouddn.com/7cdnpeizhihttps.png)
> ![](http://oqpmmru7y.bkt.clouddn.com/8fuzhicname.png)

> 3.修改域名解析记录

> ![](http://oqpmmru7y.bkt.clouddn.com/9tianjiacnamejiexi.png)

这其中会遇到的问题总结（这里只总结自己在配置https中所遇到的问题）： 

> CDN **CNAME** 解析问题，一般域名的解析中都会存在已经解析好的A记录，如果你已经把域名指向到了你的虚拟主机或者服务器。就会有这样一条记录：`A  @  默认 ip地址`

> ![](http://oqpmmru7y.bkt.clouddn.com/10yumingjiexi.png)

> 这样的话你在添加CNAME的时候,会提示**CNAME记录与主机记录（@）的A记录冲突，无法保存成功**需要删除@的这条A记录，在重新添加CNAME记录解析。

> ![](http://oqpmmru7y.bkt.clouddn.com/11jiaxihaode.png)

> 一般在十分钟左右就会生效。（如果你在配置中遇到了其他问题欢迎在[issue](https://github.com/smileyby/create-website/issues)中提问）

到这里呢，我们网站的基本配置就完成了。接下来就是建页面加内容了。

## 使用wordpress，开始搭建

在配置了https之后，安装wordpress过程中会发现，所有的css和js都加载失败了。此时需要配置一下里面function.php文件

wordpress官方给出的https配置方案：[https://wordpress.org/plugins/wordpress-https/#installation](https://wordpress.org/plugins/wordpress-https/#installation)
