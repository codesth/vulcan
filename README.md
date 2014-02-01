Vulcan Spider
======
a dynamic spider framework based on gevent and multi-threads,support webkit engine for dom parsing.

基于gevent和多线程模型，支持WebKit引擎的动态爬虫框架。

### 特性

1. 支持gevent和多线程两种并行模型
2. 支持Webkit引擎 (dom parse,ajax fetch,etc...)
3. 多个自定义选项设置

>
* 最大爬取深度限制
* 最大抓取URL数限制
* 同源（域）限制
* 自定义头部 (UA,Cookies,etc...)


### 依赖

* python 2.7
* gevent 1.0dev
* threadpool (多线程模型使用)
* lxml 2.3
* chardet 2.2.1


### 示例

    spider = Spider(concurrent_num=20,depth=3,max_url_num=300,crawler_mode=0)
    spider.feed_url("http://www.pnigos.com/")
    spider.start()

### 说明

1. 框架由两部分组成：

>
* fetcher:下载器，负责获取HTML，送入crawler。
* crawler:爬取器，负责解析并爬取HTML中的URL，送入fetcher。

fetcher和crawler两部分独立工作，互不干扰，通过queue进行链接。fetcher需要发送HTTP请求，涉及到阻塞操作，使用gevent池控制。crawler没有涉及阻塞操作，但为了扩展可以自选gevent池和多线程池两种模型控制。

2. 爬虫相关选项说明：

>
* concurrent_num    : 并行crawler和fetcher数量
* crawl_tags        : 爬行时收集URL所属标签列表
* depth             : 爬行深度限制
* max_url_num       : 最大收集URL数量
* internal_timeout  : 内部调用超时时间
* spider_timeout    : 爬虫超时时间
* crawler_mode      : 爬取器模型(0:多线程模型,1:gevent模型)
* same_origin       : 是否限制相同域下


### TODO

* URL拆分成独立部分存储(pagename,params,fragments,post data)
* webkit 支持
* 相似URL合并
* 这只是一个框架，保证了框架运行的稳定性，更多扩展就留给各位有缘人吧。


### LICENSE

Copyright © 2014 by pnig0s

Under MIT license : [rem.mit-license.org](http://rem.mit-license.org/)
