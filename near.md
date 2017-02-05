# 查询附近故事点

查询某个经纬度附近的景区、景点和故事等。

# 接口调用请求说明
```
http请求方式: GET。
https://api.fishsaying.com/story/near?access_token=ACCESS_TOKEN&lat=LAT&lng=LNG&radius=RANGE
```

# 参数说明

| 参数        | 是否必须 | 说明               |
| ---------- |---------|-------------------|
| access_token | 是      | 第一步获取到的access_token |
| lat      | 是      | 当前位置的纬度 | 
| lng      | 是      | 当前位置的经度 |
| radiu    | 否      | 当前位置附近多少米， 默认1000m， 最大10000m |


# 返回说明

正常情况下，鱼说会返回下述JSON数据包给开发者：
```
{
    "total": 2,
    "page": 1,
    "limit":10,
    "data": [
      {
        "id": "560580769a0b8ae079ad49cb",
        "title": "艾芜  受尽人间折磨",
        "location": {
          "lat": 30.833769,
          "lng": 104.110009
        },
        "cover": {
          "source": "https://image-cdn.fishsaying.com/FmYvlmKJKX5LCF_g942FRwZaJ6Ir"
        },
        "distance": 4339.659829080749,
        "author":{
            "id":"123412",
            "name":"eric",
            "avator":{
                "source": "https://image-cdn.fishsaying.com/FmYvlmKJKX5LCF_g942FRwZaJ6Ir"
            }
        },
        "voice": "https://voice-cdn.fishsaying.com/e5fa96cc4d57492c988f880232f1eaf3.m4a_trance_mp4?Expires=1486280142&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=x3oBAwnLfWdgx7%2B9J7n96zqU2Mg%3D",
        "description": "万竹园 竹子为什么是文人的最爱？\n万竹园坐落于山东省济南市趵突泉西侧，是吸取北京王府、南方庭院、济南四合院建筑特点糅合而成的古建筑群。"
      },
      {
        "id": "56057fe19a0b8a85109065e9",
        "title": "艾芜  南行之前",
        "location": {
          "lat": 30.833769,
          "lng": 104.110009
        },
        "cover": {
          "source": "https://image-cdn.fishsaying.com/FgUtyp-IzP4KpBiVrVq_i06oAzs_"
        },
        "distance": 4339.659829080749,
                "author":{
            "id":"123412",
            "name":"eric",
            "avator":{
                "source": "https://image-cdn.fishsaying.com/FmYvlmKJKX5LCF_g942FRwZaJ6Ir"
            }
        },
        "voice": "https://voice-cdn.fishsaying.com/e5fa96cc4d57492c988f880232f1eaf3.m4a_trance_mp4?Expires=1486280142&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=x3oBAwnLfWdgx7%2B9J7n96zqU2Mg%3D",
        "description": "万竹园 竹子为什么是文人的最爱？\n万竹园坐落于山东省济南市趵突泉西侧，是吸取北京王府、南方庭院、济南四合院建筑特点糅合而成的古建筑群。"
      }
    ]
  }
}
```

| 参数          | 说明                |
| ------------ |--------------------|
| access_token | 获取到的凭证          |


错误时鱼说会返回错误码等信息，JSON数据包示例如下（该示例为AppID无效错误）:
```
{ "errcode": 40014, "errmsg": "invalid parameters." }
```
           