[[Python Env Set]]

[[Xpath]]


## What happenswhen you type in a url into a browser?

dd

## httpie
- install: pip install httpie
- 查看url request response 内容：
         request：
			python -m httpie -p HBh http://www.bupt.edu.cn
			GET / HTTP/1.1
			Accept: */*
			Accept-Encoding: gzip, deflate
			Connection: keep-alive
			Host: www.bupt.edu.cn      向服务器指定域名，因为一个服务器（ip）上可能不止一个域名
			User-Agent: HTTPie/3.2.1  访问方标识（服务器、程序、爬虫。。。）
		response：
			HTTP/1.1 200 OK
			Cache-Control: private, max-age=600
			Connection: keep-alive
			Content-Encoding: gzip
			Content-Language: zh-CN
			Content-Type: text/html
			Date: Fri, 19 Aug 2022 02:19:54 GMT
			Expires: Fri, 19 Aug 2022 02:29:53 GMT
			Referer-Policy: no-referer-when-downgrade
			Server: none
			Transfer-Encoding: chunked
			Vary: User-Agent,Accept-Encoding
			X-Content-Type-Options: nosniff
			X-Download-Options: noopen
			X-Frame-Options: SAMEORIGIN
			X-Permitted-Cross-Domain-Policies: master-only
			X-XSS-Protection: 1; mode=block
			
[[Get、Post区别]]


## 查看浏览器reuest header
1. 右键打开inspect
2. 选network->Doc->左侧边栏选取一项，右键Cope curl
3.	curl内容为：
	cu r lcu rcurl 'https://search.douban.com/book/subject_search?search_text=%E7%BC%96%E7%A8%8B&cat=1001' \
	  -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9' \
	  -H 'Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7' \
	  -H 'Cache-Control: max-age=0' \
	  -H 'Connection: keep-alive' \
	  -H 'Cookie: bid=DReNqj650rs; gr_user_id=11a5fdc9-002c-4353-b257-1eea9b2d35ef; __utmc=30149280; __gads=ID=28f802dac467e8ea-22445cab23d5008a:T=1660627916:RT=1660627916:S=ALNI_MYTP7brXZ-oPfv8g6Pt263bl8JhSA; _ga=GA1.1.550702406.1660628679; _ga_RXNMP372GL=GS1.1.1660628679.1.0.1660629288.60; douban-fav-remind=1; __gpi=UID=000008a6231e06ee:T=1660627916:RT=1660714868:S=ALNI_MY_T-MDSrpLz44nJwWv7U_3OtDJ-g; viewed="25907783_26421219_2622187_20491078_10607365_21325184_24641620_26791781_26278021_26840215"; ll="108288"; ap_v=0,6.0; gr_session_id_22c937bbd8ebd703f2d8e9445f7dfd03=a987bb96-f8ff-450d-8542-bb724c9ba5a5; gr_cs1_a987bb96-f8ff-450d-8542-bb724c9ba5a5=user_id%3A0; gr_session_id_22c937bbd8ebd703f2d8e9445f7dfd03_a987bb96-f8ff-450d-8542-bb724c9ba5a5=true; __utma=30149280.2134419146.1660627927.1660627927.1660876962.2; __utmz=30149280.1660876962.2.2.utmcsr=cn.bing.com|utmccn=(referral)|utmcmd=referral|utmcct=/; __utmt_douban=1; _pk_ref.100001.2939=%5B%22%22%2C%22%22%2C1660876971%2C%22https%3A%2F%2Fbook.douban.com%2F%22%5D; _pk_id.100001.2939=e270e562696c8c61.1660629475.2.1660876971.1660629475.; _pk_ses.100001.2939=*; __utmt=1; __utmb=30149280.2.10.1660876962' \
	  -H 'Referer: https://book.douban.com/' \
	  -H 'Sec-Fetch-Dest: document' \
	  -H 'Sec-Fetch-Mode: navigate' \
	  -H 'Sec-Fetch-Site: same-site' \
	  -H 'Sec-Fetch-User: ?1' \
	  -H 'Upgrade-Insecure-Requests: 1' \
	  -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.134 Safari/537.36 Edg/103.0.1264.77' \
	  -H 'sec-ch-ua: " Not;A Brand";v="99", "Microsoft Edge";v="103", Chromium";v="103"' \
	  -H 'sec-ch-ua-mobile: ?0' \
	  -H 'sec-ch-ua-platform: "Linux"' \
	  --compressed

## Python curl request
- [将curl命令行转化为python request 封装code](https://reqbin.com/req/python/c-xgafmluu/convert-curl-to-python-requests)
- header中较为重要的iterm：
	- headers["User-Agent"]
	-  headers["Referer"]   本页面的前一页面
	-  headers["Accept"]   想要获取的文件类型（text、json...）

```
import requests

from requests.structures import CaseInsensitiveDict

url = "https://search.douban.com/book/subject_search?search_text=%E7%BC%96%E7%A8%8B&cat=1001"

headers = CaseInsensitiveDict()

headers["Accept"] = "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9"

headers["Accept-Language"] = "en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7"

headers["Cache-Control"] = "max-age=0"

headers["Connection"] = "keep-alive"

# headers["Cookie"] = "bid=DReNqj650rs; gr_user_id=11a5fdc9-002c-4353-b257-1eea9b2d35ef; __utmc=30149280; __gads=ID=28f802dac467e8ea-22445cab23d5008a:T=1660627916:RT=1660627916:S=ALNI_MYTP7brXZ-oPfv8g6Pt263bl8JhSA; _ga=GA1.1.550702406.1660628679; _ga_RXNMP372GL=GS1.1.1660628679.1.0.1660629288.60; douban-fav-remind=1; __gpi=UID=000008a6231e06ee:T=1660627916:RT=1660714868:S=ALNI_MY_T-MDSrpLz44nJwWv7U_3OtDJ-g; viewed="25907783_26421219_2622187_20491078_10607365_21325184_24641620_26791781_26278021_26840215"; ll="108288"; ap_v=0,6.0; gr_session_id_22c937bbd8ebd703f2d8e9445f7dfd03=a987bb96-f8ff-450d-8542-bb724c9ba5a5; gr_cs1_a987bb96-f8ff-450d-8542-bb724c9ba5a5=user_id%3A0; gr_session_id_22c937bbd8ebd703f2d8e9445f7dfd03_a987bb96-f8ff-450d-8542-bb724c9ba5a5=true; __utma=30149280.2134419146.1660627927.1660627927.1660876962.2; __utmz=30149280.1660876962.2.2.utmcsr=cn.bing.com|utmccn=(referral)|utmcmd=referral|utmcct=/; __utmt_douban=1; _pk_ref.100001.2939=%5B%22%22%2C%22%22%2C1660876971%2C%22https%3A%2F%2Fbook.douban.com%2F%22%5D; _pk_id.100001.2939=e270e562696c8c61.1660629475.2.1660876971.1660629475.; _pk_ses.100001.2939=*; __utmt=1; __utmb=30149280.2.10.1660876962"

headers["Referer"] = "https://book.douban.com/"

headers["Sec-Fetch-Dest"] = "document"

headers["Sec-Fetch-Mode"] = "navigate"

headers["Sec-Fetch-Site"] = "same-site"

headers["Sec-Fetch-User"] = "?1"

headers["Upgrade-Insecure-Requests"] = "1"

headers["User-Agent"] = "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.134 Safari/537.36 Edg/103.0.1264.77"

# headers["sec-ch-ua"] = "" Not;A Brand";v="99", "Microsoft Edge";v="103", "Chromium";v="103""

headers["sec-ch-ua-mobile"] = "?0"

# headers["sec-ch-ua-platform"] = ""Linux""

resp = requests.get(url, headers=headers)

resp 
```
## AJAX Json 数据提取

1. 右键打开inspect
2. 选network->Fetch/XHR->左侧边栏选取一项，右键Cope curl
3.	curl内容为：
	curl 'https://api.bilibili.com/x/web-interface/dynamic/entrance?video_offset=697766502971998200&article_offset=0&alltype_offset=0' \
  -H 'authority: api.bilibili.com' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7' \
  -H $'cookie: buvid3=4827C473-4ACF-2676-9908-EBDC326FC49919107infoc; i-wanna-go-back=-1; b_ut=7; _uuid=EFABBEB2-1528-FC31-62CD-69A1B3D784B528996infoc; buvid4=20BDC2F3-4717-9988-E6A1-EF6FBE858CB320409-022080515-BZ1x8dFmFkazAdekkmzSuA%3D%3D; nostalgia_conf=-1; CURRENT_BLACKGAP=0; rpdid=|(JYYRR)|RkR0J\'uYlmY)k)l|; PVID=1; innersign=1; fingerprint=e07bb88f4729bc27fbdd590f4a068639; buvid_fp_plain=undefined; SESSDATA=877de6cb%2C1676424422%2Cdbdc0%2A81; bili_jct=e9ce413474cc217e2468814b9d5f846d; DedeUserID=7353772; DedeUserID__ckMd5=4aebc0ebc9e5ecfc; sid=8s7s5o3o; buvid_fp=e07bb88f4729bc27fbdd590f4a068639; CURRENT_QUALITY=0; bsource=share_source_copy_link; b_lsid=5FFF4817_182CD303A6F; b_timer=%7B%22ffp%22%3A%7B%22333.1007.fp.risk_4827C473%22%3A%22182CD305CDF%22%2C%22333.337.fp.risk_4827C473%22%3A%22182C814F1EB%22%2C%22333.788.fp.risk_4827C473%22%3A%22182CD303D78%22%2C%22333.999.fp.risk_4827C473%22%3A%22182CD30555B%22%2C%22888.71577.fp.risk_4827C473%22%3A%221829F664DD9%22%2C%22888.2421.fp.risk_4827C473%22%3A%22182AFE8F3E5%22%2C%22333.42.fp.risk_4827C473%22%3A%22182B3B5B425%22%2C%22444.42.fp.risk_4827C473%22%3A%22182AFED3075%22%2C%22777.5.0.0.fp.risk_4827C473%22%3A%22182C9ACEAEA%22%2C%22333.880.fp.risk_4827C473%22%3A%22182B3B70C21%22%2C%22333.1193.fp.risk_4827C473%22%3A%22182CD305021%22%2C%22333.874.fp.risk_4827C473%22%3A%22182C9AB7370%22%7D%7D; bp_video_offset_7353772=697766502971998200; CURRENT_FNVAL=4048' \
  -H 'origin: https://space.bilibili.com' \
  -H 'referer: https://space.bilibili.com/23852932/channel/collectiondetail?sid=26384' \
  -H 'sec-ch-ua: " Not;A Brand";v="99", "Microsoft Edge";v="103", "Chromium";v="103"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "Linux"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: same-site' \
  -H 'user-agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.134 Safari/537.36 Edg/103.0.1264.77' \
  --compressed
4. json 内容
	{code: 0, message: "0", ttl: 1, data: {,…}}
	aids: [720403854, 975762798, 591026961, 548615535, 763667586, 721271869, 336478862, 634094029, 464127130,…]
	archives: [,…]
	meta: {category: 0,…}	
	category: 0
	cover: "https://archive.biliimg.com/bfs/archive/3c81cae84f47ed3bacf51a1ecfe6e413610bfa14.jpg"
	description: "我主讲的《Python编程与实践》课程，手把手带你爱上编程，爱上Python！"
	mid: 23852932
	name: "北邮《Python编程与实践》(2021)"
	ptime: 1640055739
	season_id: 26384
	total: 14
	page: {page_num: 1, page_size: 30, total: 14}
	
	