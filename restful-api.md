#接口设计

所有接口均需要带上`access_token`参数

##地理位置搜索——故事
`https://api.fishsaying.com/geo-search/stories?page={page}&limit={limit}&latitude={latitude}&longitude={longitude}&radius={radius}`

###HTTP方法
GET

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
latitude  |      double | 纬度       | 30.845942     | true
longitude  |      double | 经度       | 104.066833     | true
radius  |      int | 搜索半径(米) `1<= limit <=10,000`     | 10000     | true
page  |      int | 第几页 `default:1, page >=1`      | 1        |   false
limit  |      int | 每页记录数 `default:10, 1<= limit <=100`     | 2     | false

###Response Example
```
{
    "total": 2,
    "page": 1,
    "limit":2,
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
        "voice_link": "https://voice-cdn.fishsaying.com/e5fa96cc4d57492c988f880232f1eaf3.m4a_trance_mp4?Expires=1486280142&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=x3oBAwnLfWdgx7%2B9J7n96zqU2Mg%3D",
    	"description": "万竹园 竹子为什么是文人的最爱？\n万竹园坐落于山东省济南市趵突泉西侧，是吸取北京王府、南方庭院、济南四合院建筑特点糅合而成的古建筑群。"
      }
    ]
  }
}
```
###Response Parameters
###分页参数
   参数名  |       描述 
-------- | ----------- 
total  |      故事总数
page  |      故事从第几页返回
limit  |   本次调用获取的故事数
###故事实体
   参数名  |       描述 
-------- | ----------- 
id  |      故事ID
title  | 标题    
lat  |    故事所在纬度
lng  |    故事所在经度
source  |    故事封面图片  
distance  |    离搜索经纬度的距离(米) 
voice_link  |    故事语音链接
description | 故事描述

###故事作者

   参数名  |       描述 
-------- | ----------- 
id  |      作者ID
name  | 作者名称    
source  |    作者头像 
##地理位置搜索——景区景点
`https://api.fishsaying.com/geo-search/scenics?page={page}&limit={limit}&latitude={latitude}&longitude={longitude}&radius={radius}&type={type}`

###HTTP方法
GET

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
latitude  |      double | 纬度       | 30.845942     | true
longitude  |      double | 经度       | 104.066833     | true
radius  |      int | 搜索半径(米) maximum:10,000      | 10000     | true
page  |      int | 第几页 `default:1, page >=1`      | 1        |   false
limit  |      int | 每页记录数 `default:10, 1<= limit <=100`     | 2     | false

###Response Example
```
{
    "total": 2,
    "page": 1,
    "limit":2,
    "data": [
       {
        "id": "560580769a0b8ae079ad49cb",
        "title": "武侯祠",
        "type": 1,
        "location": {
          "lat": 30.833769,
          "lng": 104.110009
        },
        "cover": {
          "source": "https://image-cdn.fishsaying.com/FmYvlmKJKX5LCF_g942FRwZaJ6Ir"
        },
        "distance": 4339.659829080749,
    	"description": "万竹园 竹子为什么是文人的最爱？\n万竹园坐落于山东省济南市趵突泉西侧，是吸取北京王府、南方庭院、济南四合院建筑特点糅合而成的古建筑群。"
      }
    ]
  }
}
```
###Response Parameters
###分页参数
   参数名  |       描述 
-------- | ----------- 
total  |      故事总数
page  |      故事从第几页返回
limit  |   本次调用获取的故事数
###景区景点实体
   参数名  |       描述 
-------- | ----------- 
id  |      景区景点ID
title  | 景区景点标题
type  | 景区景点类型，1表示景区，2表示景点    
lat  |    景区景点所在纬度
lng  |    景区景点所在经度
source  |    景区景点封面图片  
distance  |    离搜索经纬度的距离(米) 
description | 景区景点描述

##故事关键字搜索
`https://api.fishsaying.com/search/stories?keyword={keyword}`
###HTTP方法
GET

###Request Parameters
   参数名称  |      参数类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
keyword  |      string | 关键字       | 诸葛亮     | trueid
page  |      int | 第几页 `default:1, page >=1`      | 1        |   false
limit  |      int | 每页记录数 `default:10, 1<= limit <=100`     | 2     | false

###Response Example
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
```
###Response Parameters
###分页参数
   参数名  |       描述 
-------- | ----------- 
total  |      故事总数
page  |      故事从第几页返回
limit  |   本次调用获取的故事数
###故事实体
   参数名  |       描述 
-------- | ----------- 
id  |      故事ID
title  | 标题    
lat  |    故事所在纬度
lng  |    故事所在经度
source  |    故事封面图片  
distance  |    离搜索经纬度的距离(米) 
voice_link  |    故事语音链接
description | 故事描述

###故事作者

   参数名  |       描述 
-------- | ----------- 
id  |      作者ID
name  | 作者名称    
source  |    作者头像 
##景区景点关键字搜索
`https://api.fishsaying.com/content/search?keyword={keyword}`
###HTTP方法
GET

###Request Parameters
   参数名称  |      参数类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
keyword  |      string | 关键字       | 诸葛亮     | true
page  |      int | 第几页 `default:1, page >=1`      | 1        |   false
limit  |      int | 每页记录数 `default:10, 1<= limit <=100`     | 2     | false

###Response Example
```
{
    "total": 1,
    "page": 1,
    "limit":2,
    "data": [
            {
        "id": "560580769a0b8ae079ad49cb",
        "title": "武侯祠",
        "type": 1,
        "location": {
          "lat": 30.833769,
          "lng": 104.110009
        },
        "cover": {
          "source": "https://image-cdn.fishsaying.com/FmYvlmKJKX5LCF_g942FRwZaJ6Ir"
        },
        "distance": 4339.659829080749,
    	"description": "万竹园 竹子为什么是文人的最爱？\n万竹园坐落于山东省济南市趵突泉西侧，是吸取北京王府、南方庭院、济南四合院建筑特点糅合而成的古建筑群。"
      }
    ]
}
```
###Response Parameters
###分页参数
   参数名  |       描述 
-------- | ----------- 
total  |      故事总数
page  |      故事从第几页返回
limit  |   本次调用获取的故事数
###景区景点实体
   参数名  |       描述 
-------- | ----------- 
id  |      景区景点ID
title  | 景区景点标题
type  | 景区景点类型，1表示景区，2表示景点    
lat  |    景区景点所在纬度
lng  |    景区景点所在经度
source  |    景区景点封面图片  
distance  |    离搜索经纬度的距离(米) 
description | 景区景点描述
##历史人物关键字搜索
`https://api.fishsaying.com/search/figures?keyword={keyword}`

###HTTP方法
GET

###Request Parameters
   参数名称  |      参数类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
keyword  |      string | 关键字       | 诸葛亮     | true
page  |      int | 第几页 `default:1, page >=1`      | 1        |   false
limit  |      int | 每页记录数 `default:10, 1<= limit <=100`     | 2     | false

###Response Example
```
{
    "total": 1,
    "page": 1,
    "limit":2,
    "data": [
      {
        "id": "560580769a0b8ae079ad49cb",
        "name": "诸葛亮",
        "avator": {
          "source": "https://image-cdn.fishsaying.com/FmYvlmKJKX5LCF_g942FRwZaJ6Ir"
        },
    	"description": "诸葛亮"
      }
    ]
}
```
###Response Parameters
###分页参数
   参数名  |       描述 
-------- | ----------- 
total  |      故事总数
page  |      故事从第几页返回
limit  |   本次调用获取的故事数
###历史人物实体
   参数名  |       描述 
-------- | ----------- 
id  |      历史人物ID
name  | 历史人物名
source  |    历史人物封面图片
description | 历史人物描述
##内容详情—故事
`https://api.fishsaying.com/articles/{id}`

###HTTP方法
GET

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
id  |      string | 故事ID `path parameter`       | 45c0662735e740299308b5705543c527     | true

```
{
    "id": "45c0662735e740299308b5705543c527",
    "title": "万竹园 竹子为什么是文人的最爱",
    "cover": {
      "source": "https://image-cdn.fishsaying.com/7f677e251d214dacbbff3db38a7e44e1.jpg"
    },
    "place": "万竹园",
    "scenics": [
      {
        "id": "54cdcb959a0b8ad439d05684",
        "title": "万竹园",
        "type": 2
      }
    ],
    "location": {
      "lat": 36.660476,
      "lng": 117.014031
    },
    "user": {
      "id": "00fb98d87e1543608e19f51211a8c201",
      "username": "诗鱼远方",
      "avatar": {
        "source": "https://image-cdn.fishsaying.com/29b95c6cf1b04c9d9932093c6bd6544f.jpg"
      }
    },
    "voice_link": "https://voice-cdn.fishsaying.com/e5fa96cc4d57492c988f880232f1eaf3.m4a_trance_mp4?Expires=1486281498&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=KbgYSvQZTcMPaOpRTzIEad2gl/U%3D",
    "length": 1000,
    "description": "万竹园 竹子为什么是文人的最爱？"
}

```
###Response Parameters
###故事实体
   参数名  |       描述 
-------- | ----------- 
id  |      故事ID
title  | 标题    
source  |    故事封面图片
place  |    故事所在地  
lat  |    故事所在纬度
lng  |    故事所在经度 
voice_link  |    故事语音链接
length  |    故事语音时长
description | 故事描述
###景区景点实体

   参数名  |       描述 
-------- | ----------- 
id  |      景区景点ID
title  | 景区景点名称    
type  | 景区景点类型，1表示景区，2表示景点  
###故事作者

   参数名  |       描述 
-------- | ----------- 
id  |      作者ID
name  | 作者名称    
source  |    作者头像 
##内容详情—景区景点
`https://api.fishsaying.com/scenics/{id}`

###HTTP方法
GET

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
id  |      string | 景区景点ID `path parameter`       | 54d896539a0b8a283ff43186     | true

```
{
    "id": "54d896539a0b8a283ff43186",
    "title": "文臣廊",
    "address": "四川省成都市武侯区浆洗街街道章武街12号 邮政编码: 510107",
    "cover": {
      "source": "https://image-cdn.fishsaying.com/FrHrryp5kLkVgwXkgMNbMmB-drJh"
    },
    "location": {
      "lat": 30.645446,
      "lng": 104.049703
    },
    "type": 2,
    "voice_total": 83,
    "description": ""
}

```
###Response Parameters
###景区景点实体
   参数名  |       描述 
-------- | ----------- 
id  |      景区景点ID
title  | 景区景点名称    
address  |    景区景点详细地址
source  |    景区景点封面图片
lat  |    故事所在纬度
lng  |    故事所在经度 
type  | 景区景点类型，1表示景区，2表示景点 
voice_total  |    景区景点下故事总数
description | 景区描述

##内容详情—历史人物
`https://api.fishsaying.com/figures/{id}`
###HTTP方法
GET

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
id  |      string | 历史人物ID `path parameter` | 54cf571c9a0b8abc1aba39a5     | true

```
{
    "id": "54cf571c9a0b8abc1aba39a5",
    "name": "孟获",
    "sex": 0,
    "start": "99999999",
    "end": "99999999",
    "ancients": [
      {
        "region": "亚洲",
        "ancient": "",
        "dynasty": "三国"
      }
    ],
    "avatar": {
      "source": "https://image-cdn.fishsaying.com/FnBA2O4oIR9-yq9XDPlXJKvq1TEi"
    },
    "nicknames": []
}

```
###Response Parameters
###历史人物实体
   参数名  |       描述 
-------- | ----------- 
id  |      历史人物ID
name  | 历史人物名称
sex | 历史人物性别 0:男,1:女
start  |    出生年，`99999999 表示不详`
end  |    卒年，`99999999 表示不详`
region  |  所属区域
ancient  |  
dynasty  | 所属朝代 
source  |    历史人物封面图片
nicknames | 其它称谓

##景区景点关联的故事列表
`https://api.fishsaying.com/scenics/{scenicid}/articles?page={page}&limit={limit}`

###HTTP方法
GET

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
scenicid  |  string | 景区景点ID       | 54f424399a0b8afc44174e2c     | true
page  |      int | 第几页 `default:1, page >=1`      | 1        |   false
limit  |      int | 每页记录数 `default:10, 1<= limit <=100`     | 2     | false

###Response Example
```
{
    "total": 26,
    "page": 1,
    "limit":10,    
    "data": [
      {
        "id": "56319b569a0b8aa52006834a",
        "title": "淡岛堂 感谢缝衣针的辛勤付出",
        "cover": {
          "source": "https://image-cdn.fishsaying.com/Fjao177iTEY7X9XdlYwcxAN8tBSi"
        },
        "place": "淡岛堂",
        "voice": "https://voice-cdn.fishsaying.com/FpUdjuGpKdzPvvNBTKA3ByEFEKla_trance_mp4?Expires=1486282474&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=%2Bx%2BIP1AnQDSahb3TiJe988WzPs0%3D",
        "length": 1000,
        "user": {
          "id": "55e00f0d7f944046008b69de",
          "name": "仙人掌的刺",
          "avatar": {
            "source": "https://image-cdn.fishsaying.com/29b95c6cf1b04c9d9932093c6bd6544f.jpg"
          }
        }
      },
      {
        "id": "56319acc7f9440286c8b4afa",
        "title": "宝藏门 总是遭受火灾",
        "cover": {
          "source": "https://image-cdn.fishsaying.com/FiC_8kdNnwGMuREGX_IcxQv5X8fT"
        },
        "place": "宝藏门",
        "voice": "https://voice-cdn.fishsaying.com/Fva_cBuHy43XOFRjdVDY8PnTjgnM_trance_mp4?Expires=1486282474&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=Qos3S1%2BA90hR5wwX/JtlefAIgyI%3D",
        "length": 107,
        "user": {
          "id": "55e00f0d7f944046008b69de",
          "name": "仙人掌的刺",
          "avatar": {
            "source": "https://image-cdn.fishsaying.com/29b95c6cf1b04c9d9932093c6bd6544f.jpg"
          }
        }
      }
    ]
}
```
###Response Parameters
###分页参数
   参数名  |       描述 
-------- | ----------- 
total  |      故事总数
page  |      故事从第几页返回
limit  |   本次调用获取的故事数
###故事实体
   参数名  |       描述 
-------- | ----------- 
id  |      故事ID
title  | 标题    
lat  |    故事所在纬度
lng  |    故事所在经度
source  |    故事封面图片  
distance  |    离搜索经纬度的距离(米) 
voice_link  |    故事语音链接
description | 故事描述

###故事作者

   参数名  |       描述 
-------- | ----------- 
id  |      作者ID
name  | 作者名称    
source  |    作者头像 

##历史人物关联的故事列表
`https://api.fishsaying.com/figures/{figureid}/articles?page={page}&limit={limit}`

###HTTP方法
GET

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
figureid  |  string | 历史人物ID       | 54d183ef9a0b8a534f414469     | true
page  |      int | 第几页 `default:1, page >=1`      | 1        |   false
limit  |      int | 每页记录数 `default:10, 1<= limit <=100`     | 2     | false

###Response Example
```
{
    "total": 26,
    "page": 1,
    "limit":10,    
    "data": [
      {
        "id": "56319b569a0b8aa52006834a",
        "title": "淡岛堂 感谢缝衣针的辛勤付出",
        "cover": {
          "source": "https://image-cdn.fishsaying.com/Fjao177iTEY7X9XdlYwcxAN8tBSi"
        },
        "place": "淡岛堂",
        "voice": "https://voice-cdn.fishsaying.com/FpUdjuGpKdzPvvNBTKA3ByEFEKla_trance_mp4?Expires=1486282474&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=%2Bx%2BIP1AnQDSahb3TiJe988WzPs0%3D",
        "length": 1000,
        "user": {
          "id": "55e00f0d7f944046008b69de",
          "name": "仙人掌的刺",
          "avatar": {
            "source": "https://image-cdn.fishsaying.com/29b95c6cf1b04c9d9932093c6bd6544f.jpg"
          }
        }
      },
      {
        "id": "56319acc7f9440286c8b4afa",
        "title": "宝藏门 总是遭受火灾",
        "cover": {
          "source": "https://image-cdn.fishsaying.com/FiC_8kdNnwGMuREGX_IcxQv5X8fT"
        },
        "place": "宝藏门",
        "voice": "https://voice-cdn.fishsaying.com/Fva_cBuHy43XOFRjdVDY8PnTjgnM_trance_mp4?Expires=1486282474&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=Qos3S1%2BA90hR5wwX/JtlefAIgyI%3D",
        "length": 107,
        "user": {
          "id": "55e00f0d7f944046008b69de",
          "name": "仙人掌的刺",
          "avatar": {
            "source": "https://image-cdn.fishsaying.com/29b95c6cf1b04c9d9932093c6bd6544f.jpg"
          }
        }
      }
    ]
}
```
###Response Parameters
###分页参数
   参数名  |       描述 
-------- | ----------- 
total  |      故事总数
page  |      故事从第几页返回
limit  |   本次调用获取的故事数
###故事实体
   参数名  |       描述 
-------- | ----------- 
id  |      故事ID
title  | 标题    
lat  |    故事所在纬度
lng  |    故事所在经度
source  |    故事封面图片  
distance  |    离搜索经纬度的距离(米) 
voice_link  |    故事语音链接
description | 故事描述

###故事作者

   参数名  |       描述 
-------- | ----------- 
id  |      作者ID
name  | 作者名称    
source  |    作者头像 

