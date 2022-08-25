[# 北邮《Python编程与实践》课程 (2020)](https://www.bilibili.com/video/BV1b7411N7P2?p=30&vd_source=7e2c68310006ca594a21fb9d90a89e0f)


## 12讲 爬虫框架初步
### [[Regex]]
### 13讲 豆瓣爬虫进化
- regex
- 遍历list本身需要修改时，可用range index遍历
	```
	for index in range(len(result)):
		del result[index][4]
		result[index].extend(aaa)

	```
## 14讲  爬虫进阶 DOM XPATH
- [[The Hitchhiker's Guide to Python]]
- `dir(object)`可以查看对象实例的方法
	`book_name_elem.attrib?`使用“？”显示该属性的细节
	![attrib?](/attrib?.jpg)
## 15讲 翻页爬取和采集目标分析方法
- xpath 中使用`text()`返回str,xpath对象使用`.text`返回str
- xpath 一般返回一个`list`，所以一般取`object[0]`
- xpath list 不支持`list[-1]`,可以使用`list[last()]`
- url encode 将url中的中文字符进行编码，形成最终访问解析的域名
 ![url encode](/urlencode.jpg)
 - 可以通过tag等页面进行全量采集
## 16讲 多线程
- [[multi_thread]]


## 17讲 深入多线程
- str format
	- "sssssss{k}.format(v)"
	- f"ssssss{v}" python3.6
- 非定向爬虫 更鲁棒的爬取海量网页
- 定向爬虫：通过研究单个网页特征爬取单个网页
## 18讲 带任务队列的多线程
- ![crawler structure](/crawler.jpeg)
- Message Queue
- [[VS Code Jypyter Lab]]  内容较多时restart 重置cell
- function中使用全局变量最好在function开始声明为global变量，否则在function中对变量进行修改，则该变量即变为局部变量。