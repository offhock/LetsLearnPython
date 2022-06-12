# 데이터 분석) 파이썬을 이용한 서울시 이디야, 스타벅스 매장 위치 분석

본 내용은 아래의 유투브를 보고 실습한 내용을 정리한 것이다.

> 유투브: https://youtu.be/qobe7k1CmGc
> 


## 위도 경도

https://python.hotexamples.com/examples/geopy.geocoders/Nominatim/-/python-nominatim-class-examples.html

```python
import requests
import urllib

def get_nominatim_geocode(address):
    url = 'https://nominatim.openstreetmap.org/search/' + urllib.parse.quote(address) + '?format=json'
    try:
        response = requests.get(url).json()
        return response[0]["lon"], response[0]["lat"]
    except Exception as e:
        # print(e)
        return None, None

for idx, rows in tqdm(df_coffee.iterrows()):
    #print(rows["주소"])
    tmp =  get_nominatim_geocode(rows["주소"].split("(")[0])
    if tmp:
        lon = tmp[0]
        lat = tmp[1]
        df_coffee.loc[idx, "위도"] = lat
        df_coffee.loc[idx, "경도"] = lon    
    else:
        print(idx, rows["주소"])
    
```
