# appstore爬虫

```python
from requests.exceptions import RequestException
import requests
import re
import json

headers = {
    'accept': 'application/json',
    'accept-encoding': 'gzip, deflate, br',
    'accept-language': 'en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7',
    'authorization': 'Bearer eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IldlYlBsYXlLaWQifQ.eyJpc3MiOiJBTVBXZWJQbGF5IiwiaWF0IjoxNTgxMDM0OTI1LCJleHAiOjE1OTY1ODY5MjV9.GHuK3wnRsuXWgHcWnPH7x_eLE82lG11_Zu5pmUvzH-OlunoHqGj3ItgAWwaOg3-fmYPnfRhfu59-mfhf5beZiw',
    'content-type': 'application/x-www-form-urlencoded; charset=UTF-8',
    'origin': 'https://apps.apple.com',
    'referer': 'https://apps.apple.com/cn/app/%E9%92%89%E9%92%89/id1435447041?mt=12',
    'sec-fetch-mode': 'cors',
    'sec-fetch-site': 'same-site',
    'User-Agent': 'Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.62 Safari/537.36'
}

def get_one_page(url):
    try:
        response = requests.get(url,headers = headers)
        if response.status_code == 200:
            return response.text
        return None
    except RequestException:
        return None
    
def write_to_file(html):
    with open('100000.json','a',encoding='utf-8') as f: 
        f.write(html)
        f.close()
    
def main(offset):
    url = 'https://amp-api.apps.apple.com/v1/catalog/cn/apps/930368978/reviews?l=zh-Hans-CN&offset=' + str(offset)+ '&platform=web&additionalPlatforms=appletv%2Cipad%2Ciphone%2Cmac'
    html = get_one_page(url)
    print(html)
    write_to_file(html)
    
if __name__ =='__main__':
    for i in range(10000,50000):
        main(i*10)
```