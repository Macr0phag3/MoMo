## 简介

最近在用`墨墨背单词`这个单词软件，各方面做的都很好。可惜存在单词上限，每背一个单词，就少一个，如果没有任何增加单词上限的途径的话，只能背500个单词你就可以删软件了。。

除了签到以及印章连连看的方式之外，还有没有增加上限的途径呢？是有的，就是每次打完卡之后可以对当日的学习情况进行分享。这个页面一旦被浏览过一次，你的单词上限就会+1（当然，一个ip只算一次），每日上限20个。于是我就写了一个自动刷访问量的脚本，原本是单线程的，很慢，后来再修改了一下弄成多线程的了。大体思路是：

1. 去免费代理ip网站爬代理
2. 利用代理访问文章
3. 增加访问量

多线程利用的自然是生产者-消费者模型。实现得有点简陋，正好最近在线程进程这边补缺补漏，就当练手了吧。

均在linux下运行（unix或许也行

需要安装：

`pip install termcolor`

 MoMo-aiohttp.py在Py3.x下运行，需要安装aiohttp
 
### 版本

1. `MoMo.py` 自己实现的多线程访问
2. `MoMo-aiohttp.py` 利用aiohttp实现的协程访问（在数量较小的情况下，和1差不多，但是数量上去了，差别会越来越大）

## 运行示例

![example](https://github.com/Macr0phag3/MoMo/blob/master/PicForREADME/example.png)

 在MoMo-aiohttp.py中，
 async with session.get(url='', proxy='http://'+proxy, timeout=5) as resp: # Your url
 url需要改，怎么获得这个呢？首先你打卡之后，要分享到空间去，然后点开这个分享，转发链接到“我的电脑“，然后你就能看到这个url，大概是这样：
 https://www.maimemo.com/share/page/?uid=XXXXXXX&pid=1181
 其中pid是每天都+1的，uid就是你的墨墨UID，在“我的设置“中可以看到
 设置好了之后再跑跑看

## 声明
本项目仅用于个人学习测试使用，勿用于非法用途，由于其他用途所产生的一切不良后果本人概不负责。

## 2018-08-24 更新
墨墨修改分享的 url 了，现在开始每天的文章用 `pid` 区分。uid 同样为墨墨UID。暂时没找到生成 pid 的方法，不过没事，每次运行改一下 pid 就行

## 2018.11.19 19:24:18 更新
http://www.66ip.cn/mo.php?tqsl=100 这个免费 ip 地址，原来是在源码中直接显示的 ip，现在估计爬的人太多了，改为运行一段 js 后才显示 ip。所以需要根据 js 写对应的 python 解析脚本。当然，最好换其他家的免费代理 ip，或者自己搭一个免费 ip 爬取系统，github 有很多这样的。

![](https://github.com/Macr0phag3/MoMo/blob/master/PicForREADME/2018-11-19_19-27-21.png)

最多改一下地址与正则表达式就行了。

## 2019.02.25 20:31:05 更新
如果出现以下报错，请关闭系统的代理再试一下。
```
» python MoMo-aiohttp.py
[+] get proxy...
  [-]Error: HTTPConnectionPool(host='127.0.0.1', port=7890): Max retries exceeded with url: http://www.89ip.cn/tqdl.html?num=100 (Caused by ProxyError('Cannot connect to proxy.', RemoteDisconnected('Remote end closed connection without response',)))
```





