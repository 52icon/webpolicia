# WebPolicia
## 命名
WebPolica 直译为"网站警察"，它是一个高效的跨平台的扫描违法网站的工具，现已支持扫描待查IP的所有端口，并访问其端口获取详细信息，之后与数据库中的关键词进行比对。

## 由来
面对严峻的网络安全形势，数据中心日常需要自查，自检，做到"know your customer"(了解你的客户，具体是验证客户的身份、适合性、和与该客户维持商业关系所带来的风险)。
其中Web服务更是高危地段，被动态势感知以及防火墙并不能很好的鉴别与发现伪装的违法网站，大多数违法网站会使用反向代理之类的工具，以达到绕过机房被动态势感知以及防火墙的目的。
传统的态势感知流程为:

+ 过滤到Web通信  -->   检测其内容   -->    记录关键词扫描结果

而WebPolicia的检测流程为

+ 使用Web服务主动检测  -->  获取返回信息  -->  检测其内容  -->  记录关键词扫描结果

## 特点
+ WebPolicia会依次构造包含域名的请求访问被测试机，若被测试机返回数据，则开始检测。
+ WebPolicia还可以针对高位端口/不常见端口进行Web服务探测，默认为全端口探测
+ 在全端口探测模式下，平均20s就可以探测完毕一个IP的所有端口的开放情况 (主机配置 Xeon Gold 6140 @ 2.3Ghz)
+ 自动化检测系统，解放运维双手





## 注意事项
国内的数据中心使用域名建设网站需要在机房的域名白名单上添加白名单信息，俗称域名过白，这样我们可以得到接入此数据中心的每个域名。



## 使用方法
UI界面的前三个选项
```{UI}
1) 导入目标IP地址 
2) 导入待查域名 
3) 导入过滤关键词
```
均为导入相关信息

1）用于导入待查IP地址，有自动监测IP合法性的功能，同时支持IP段导入，举个例子，输入172.18.50.1-10，这将会导入10个待查IP地址

2）用于导入待查域名。针对国内的数据中心，待查域名可以在机房白名单上获取，如果相关数据中心没有域名过白服务，可以为空，将直接检测IP，缺点是精度不如带域名白名单的数据中心高

⚠注意,WebPolicia每次启动会检测待查域名列表是否为空，为空会发送警告信息

3）用于导入过滤关键词。目前WebPolicia自带一份词库，由于一些原因，故不提供完整词库，请自行编写。

```{UI}
4) 查看Web服务IP与端口
```
4）用于查看执行过"扫描IP表内的所有开放端口"的结果，通常是在执行**选项5**后运行，由于这个为非必要选项，故放在第四位。

```{UI}
5) 扫描IP表内的所有开放端口          
6) 扫描并记录违规Web服务
```

5）用于扫描由**选项1**导入的IP地址上所开放的所有端口信息

6）用于扫描由**选项5**得到的开放端口信息上是否有违法信息，同时记录违法信息，并生成一份网页报告（报告在程序运行目录下的PossibleTarget.html）
          
```{UI}
7) 自动巡检
```
7）用于解放运维的双手，一次设置后，请保持窗口持续运行，Windows可以最小化CMD窗口，Linux可以使用nohup或者screen防止程序中断运行，程序将会按照设置的间隔时间，不断运行，只需运维定期去查看Web报告

```{UI}
8) 清空菜单
```
8）用于清空相关数据，例如: 待查IP地址、待查域名、过滤关键词、所有的开放端口信息、扫描报告。以及有一键清空所有内容（约等于手机上的恢复出厂设置）

## 配置邮件提醒

**现已支持:QQ邮箱 163邮箱**

QQ邮箱配置SMTP教程:https://www.baidu.com/s?ie=UTF-8&wd=qq%E9%82%AE%E7%AE%B1%E5%BC%80%E5%90%AFSMTP

163邮箱配置SMTP教程:http://help.163.com/09/1223/14/5R7P6CJ600753VB8.html?servCode=6010376

修改config.json文件
```{JSON}
{
    "UseEmail" : "1",                               #0为关闭邮件提醒功能，1为开启邮件提醒功能
    "Sender" : "webpolicia@ceshi.com",              #发件邮箱
    "Receiver" : "test@ceshi.com",                  #收件邮箱
    "SenderAccount" : "webpolicia@ceshi.com",       #发件邮箱登录账号
    "SenderPasswd" : "qazwsxedcrfv",                #发件邮箱登录密码
    "SMTPServer" : "qq"                             #发信服务器，支持qq和163，默认qq
}
```





举个例子，如果我是一名运维人员，我下载压缩包并解压后，我将会运行python ./Main.py文件启动WebPolicia，这时WebPolicia将会有一个自检进程启动，当自检通过后，我将会使用 **选项1** 添加我所管辖的服务器IP地址，之后我将从机房白名单系统上下载待查域名并且使用 **选项2** 导入系统，接下来我会使用 **选项3** 导入我所想检查的关键词，然后使用 **选项5** 来启动扫描IP端口，待扫描结束后，我会使用 **选项4** 确认一下扫描结果，接下来我将会使用 **选项6** 扫描违法网站内容。漫长的等待后，我将会在程序目录下得到一个PossibleTarget.html扫描报告，接下来我可以随时查阅此报告。
处理掉现有违法网站后，我需要定期复查，我会使用 **选项7** 自动巡检。





## 预览
支持跨平台

<p align="center">
  <a href="https://github.com/52icon/webpolicia/raw/main/UI_Linux.png" target="_blank">
    <img  src="https://github.com/52icon/webpolicia/raw/main/UI_Linux.png">
  </a>
  <a href="https://github.com/52icon/webpolicia/raw/main/UI_Windows.png" target="_blank">
    <img  src="https://github.com/52icon/webpolicia/raw/main/UI_Windows.png">
  </a>    
</p>

邮件提醒会根据是否扫描出可疑目标更换标题
<p align="center">
  <a href="https://github.com/52icon/webpolicia/raw/main/Email1.png" target="_blank">
    <img width="300px" src="https://github.com/52icon/webpolicia/raw/main/Email1.png">
  </a>
 <a href="https://github.com/52icon/webpolicia/raw/main/Email2.png" target="_blank">
    <img width="300px" src="https://github.com/52icon/webpolicia/raw/main/Email2.png">
  </a>
</p>

