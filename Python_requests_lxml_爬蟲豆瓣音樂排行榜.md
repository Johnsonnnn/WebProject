# Python requests+lxml 爬蟲豆瓣音樂排行榜

1. 載入資源
```bash
import requests
from lxml import etree
```

2. 下載並解析html
```bash
res = requests.get('https://music.douban.com/chart', headers=headers)

headers={'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.190 Safari/537.36'}

content = res.content.decode()
```

3. 將 html 轉為 lxml 形式
```bash
html = etree.HTML(content)
```

4. 從網頁複製Xpath路徑:
> F12>對想要的內容按右鍵>Copy>Copy XPath
> ![](https://i.imgur.com/Dew2Stt.jpg)


5. 貼到 ```html.xpath()``` 後面加上 ```/text()```顯示標籤的內容(歌名)
![](https://i.imgur.com/ZteZYEy.jpg)


```bash
main_data = html.xpath('//*[@id="content"]/div/div[1]/div/ul/li/div//a/text()')
```

6. 抓取創作者和播放量並且過濾空行和分開創作者與播放量
![](https://i.imgur.com/fjecO5N.jpg)

```bash
describe = [x.split('\xa0/\xa0') for x in list(filter(lambda x:x!='', [x.strip() for x in html.xpath('//*[@id="content"]/div/div[1]/div/ul/li/div/p/text()')]))]
```