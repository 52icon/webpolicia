# WebPolicia
## 命名
WebPolica 直译为"网站警察"，它是一个高效的跨平台的扫描违法网站的工具，现已支持扫描IP的所有端口，并访问其端口获取详细信息，之后与数据库中的关键词进行比对。

## 由来
面对严峻的网络安全形势，数据中心日常需要自查，自检，做到"know your customer"(了解你的客户，具体是验证客户的身份、适合性、和与该客户维持商业关系所带来的风险)。
其中Web服务更是高危地段，被动态势感知以及防火墙并不能很好的鉴别与发现稍加伪装的违法网站，大多数违法网站会使用反向代理之类的工具，以达到绕过机房被动态势感知以及防火墙的目的。
传统的态势感知流程为:

+ 过滤到Web通信  -->   检测其内容   -->    记录关键词扫描结果

而WebPolicia的检测流程为

+ 使用Web服务主动检测  -->  获取返回信息  -->  检测其内容  -->  记录关键词扫描结果

## 特点
+ WebPolicia会依次构造包含域名的请求访问被测试机，若被测试机返回数据，则开始检测。
+ WebPolicia还可以针对高位端口/不常见端口进行Web服务探测，默认为全端口探测
+ 在全端口探测模式下，平均20s就可以探测完毕一个IP的所有端口的开放情况 (主机配置 Xeon Gold 6140 @ 2.3Ghz)





## 注意事项
国内的数据中心使用域名建设网站需要在机房的域名白名单上添加白名单信息，俗称域名过白，这样我们可以得到接入此数据中心的每个域名。

## 介绍
支持跨平台

![UI界面](https://github.com/52icon/webpolicia/raw/main/UI_Linux.png)
![UI界面](https://github.com/52icon/webpolicia/raw/main/UI_Windows.png)
