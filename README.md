﻿# IPProxys

IPProxys代理池项目，提供代理ip。使用python2.7.x开发

## 作者博客
http://www.cnblogs.com/qiyeboy/p/5693128.html

##项目依赖

####ubuntu,debian下

安装sqlite数据库(一般系统内置):

> apt-get install sqlite3

安装requests库:

> pip install requests

安装chardet库:

> pip install chardet

安装lxml:

> apt-get install python-lxml

安装gevent库:

> pip install gevent

######(有时候使用的gevent版本过低会出现自动退出情况，请使用pip install gevent --upgrade更新)

####windows下

下载[sqlite](http://www.sqlite.org/download.html),路径添加到环境变量

安装requests库:

> pip install requests

安装chardet库:

> pip install chardet

安装lxml:

> pip install lxml或者下载[lxml windows版](https://pypi.python.org/pypi/lxml/)

安装gevent库:

> pip install gevent

######(有时候使用的gevent版本过低会出现自动退出情况，请使用pip install gevent --upgrade更新)

## 如何使用

将项目目录clone到当前文件夹

> $ git clone 

切换工程目录

```
$ cd IPProxys
```

运行脚本

```
python IPProxys.py
```

## API 使用方法

#### 模式
```
GET /
```

####参数 


| Name | Type | Description |
| ----| ---- | ---- |
| types | int | 0: 高匿代理, 1 透明 |
| protocol | int | 0: http, 1 https |
| count | int | 数量 |
| country | str | 国家 |
| area | str | 地区 |



#### 例子

#####IPProxys默认端口为8000

#####如果是在本机上测试：

1.获取5个ip地址在中国的高匿代理：http://127.0.0.1:8000/?types=0&count=5&country=中国

2.响应为JSON格式，按照响应速度由高到低，返回数据：

```
[{"ip": "220.160.22.115", "port": 80}, {"ip": "183.129.151.130", "port": 80}, {"ip": "59.52.243.88", "port": 80}, {"ip": "112.228.35.24", "port": 8888}, {"ip": "106.75.176.4", "port": 80}]
```

```
import requests
import json
r = requests.get('http://127.0.0.1:8000/?types=0&count=5&country=中国')
ip_ports = json.loads(r.text)
print ip_ports
ip = ip_ports[0]['ip']
port = ip_ports[0]['port']
proxies={
    'http':'http://%s:%s'%(ip,port),
    'https':'http://%s:%s'%(ip,port)
}
r = requests.get('http://ip.chinaz.com/',proxies=proxies)
r.encoding='utf-8'
print r.text
```

## TODO
1.添加对Python3.x的支持

2.可自主选择添加squid反向代理服务器，简化爬虫配置

3.重构HTTP API接口

4.增加更多代理网站和数据库适配

## 更新进度
-----------------------------2016-11-24----------------------------
<br/>
1.增加chardet识别网页编码
<br/>
2.突破66ip.cn反爬限制
<br/>
-----------------------------2016-10-27----------------------------
<br/>
1.增加对代理的检测，测试是否能真正访问到网址，实现代理
<br/>
2.添加通过正则表达式和加载插件解析网页的方式
<br/>
3.又增加一个新的代理网站
<br/>

-----------------------------2016-7-20----------------------------
<br/>
1.修复bug ,将数据库进行压缩
<br/>
