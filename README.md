# WebPolicia
## 命名
WebPolica 直译为"网站警察"，它是一个高效的扫描违法网站的工具，现已支持扫描IP的所有端口，并访问其端口获取详细信息，之后与数据库中的关键词进行比对。

## 由来
面对严峻的网络安全形势，数据中心日常需要自查，自检，做到"know your customer"(了解你的客户，具体是验证客户的身份、适合性、和与该客户维持商业关系所带来的风险)。
其中Web服务更是高危地段，被动态势感知以及防火墙并不能很好的鉴别与发现稍加伪装的违法网站，大多数违法网站会使用反向代理之类的工具，以达到绕过机房被动态势感知以及防火墙的目的。
传统的态势感知流程为
