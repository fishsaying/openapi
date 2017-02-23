#HTTP头 说明
用户每天接口访问的次数是有限制的，每天凌晨0点重置。下面为限流表，每个正常返回的接口响应头部都会出现以下三个自定义头，来表示本次访问后今天剩余调用次数的信息.

http header | 说明
------ | -----
X-RateLimit-Limit | 每天请求次数上限
X-RateLimit-Remaining | 今天剩余请求次数
X-RateLimit-Reset | 剩余请求次数重置剩余时间(秒)

#错误码  说明
调用鱼说提供的开放接口，如果请求参数有误或服务器异常均会响应错误返回码，正常返回则直接返回内容不会有返回码，开发这可以根据返回码信息调试接口，排查错误。
返回码说明如下：

返回码 | 说明
----- | ----
404   | `not found resource` 找不到资源
4001   | `illegal arguments` 超过约定范围阈值,如范围搜索接口中参数radius必须小于100,000
4002   | `access_token illegal or expired` access_token非法或过期
4003   | `no access_token` 没有access_token
40010  | `illegal request argument` 非法请求参数,如超过int最大值，将字符传给int参数等
40011   | `page * limit must lte 10000` elasticsearch index.max\_result_window which defaults to 10000
5001   | `api gateway exception` api网关异常
5002   | `auth server exception` 授权服务器异常

#其它注意事项
1. 为了防盗链，所有接口返回的语音链接(voice)一个小时过期，每次访问故事相关接口均会刷新url链接
2. 历史人物生卒年，`99999999`表示生卒年不详

#开放接口 说明

##获取access_token
`https://api.fishsaying.com/oauth/token?client_id={client_id}&client_secret={client_secret}&grant_type=client_credentials&scope=read`

###HTTP方法
POST

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
client_id  |  string   | 客户ID   | fs349330887550177281   | true
client_secret  |  string | 客户密钥   | JTbH3VYinLfvwMp8Aj88Z861bUSWYH1R| true
grant_type |string | 授权模式 `现只支持client_credentials模式`|client_credentials |true
scope  |  string | 权限范围 `现只支持read权限`     | read |true


###Response Example
```
{
  "access_token": "12d6daeb-b2d8-4b64-a20a-9772509ae62a",
  "token_type": "bearer",
  "expires_in": 3599,
  "scope": "read"
}
```

###Response Parameters
###响应参数
   参数名  |       描述 
-------- | ----------- 
access_token|   访问令牌
token_type  |   令牌类型
expires_in  |   过期时间(秒)
scope       |   访问权限范围

##地理位置搜索——故事
`https://api.fishsaying.com/stories/geo-search?page={page}&limit={limit}&latitude={latitude}&longitude={longitude}&radius={radius}&access_token={access_token}`

###HTTP方法
GET

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
latitude  |      double | 纬度       | 24.8459     | true
longitude  |      double | 经度       | 104.3212     | true
radius  |      int | 搜索半径(米) `1<= radius <=100,000`     | 10000     | true
page  |      int | 第几页 `default:1, page >=1`      | 1        |   false
limit  |      int | 每页记录数 `default:10, 1<= limit <=100`     | 20   | false
access_token | string | 访问令牌 | 6e229bee-9cd8-4bf3-a610-8540672fc073 | true

###Response Example
```
{
  "total": 2,
  "page": 1,
  "size": 2,
  "data": [
    {
      "id": "569e37d37f9440933c8b6446",
      "title": "罗平 生物群与三叠纪生物的接触",
      "location": {
        "lat": 24.884626,
        "lng": 104.308675
      },
      "cover": "https://image-cdn.fishsaying.com/FmwayQ57KWJkct35QBCFfwfcdVMw",
      "distance": 4490,
      "author": {
        "name": "红色高跟鞋",
        "avator": "https://image-cdn.fishsaying.com/FmfR6GQMjs1lNA5xLfsitwjLmxdU"
      },
      "voice": "https://voice-cdn.fishsaying.com/FpunapYvGUWZ9e6okGyhAF-4b-x0_trance_mp4?Expires=1487819545&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=qIBXqP/7kMtlrOo2QdeNHUoRQ%2B8%3D",
      "voiceTime": 94,
      "voiceSize": 1490885,
      "description": "三叠纪是地质纪年的一个时期，在距今2.4亿年前，看起来是个遥不可及的时期，但是在云南省罗平县，却可以亲身体会到2.4亿年前的三叠纪，与三叠纪生物来一次亲密接触。\r\n在三叠纪的时候，罗平还只是一片汪洋大海，后来由于地质活动中的造山运动，罗平不断升高，海洋逐渐退出罗平，罗平就抬高为陆地，而那些三叠纪时期死亡的海洋生物的骸骨因为累积在海底的泥土之中，而在随着陆地的抬高过程之中也浮现出来了。于是如今罗平的山地之中就藏有大量的三叠纪的海洋生物，明显地暴露在山地表面，一眼就可以看到，而且这些海洋生物遗骸都是更具时间的早晚而累积的，在山地越高的地方的海洋生物是距今年代最近的，而越往下的则是越古老的生物，所以纵观这些海洋生物遗骸化石，就像是亲历了这些生物的进化历程。\r\n而除了山地上面暴露出来的生物群，在罗平的地层之中亦有着更加久远的海洋生物化石，越往下挖掘，生物的造型更加奇异，甚至还挖出过一个长得像龙一样小鱼化石，这可比看科幻片来得真实多了。看到罗平的这些远古的生物群化石，才会惊觉地球历史的久远，而有人类存在的历史只是沧海之中的一粟罢了。"
    },
    {
      "id": "42910dd27b2543369214cfd45850f109",
      "title": "罗平县 金玉满堂之乡",
      "location": {
        "lat": 24.884626,
        "lng": 104.308675
      },
      "cover": "https://image-cdn.fishsaying.com/d8a1936474b74b3593b3ebe1ce1baf7f.jpg",
      "distance": 4490,
      "author": {
        "name": "电子科大012",
        "avator": "https://image-cdn.fishsaying.com/29b95c6cf1b04c9d9932093c6bd6544f.jpg"
      },
      "voice": "https://voice-cdn.fishsaying.com/ec3c526acf994c14b5d0d13ef8152fb7.mp3_trance_mp4?Expires=1487819545&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=%2BNolbIkvxPg/vUoWoP9qGBcp/uc%3D",
      "voiceTime": 167,
      "voiceSize": 365378,
      "description": "罗平县 金玉满堂之乡"
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
size  |   本次调用获取的故事数
###故事实体
   参数名  |       描述 
-------- | ----------- 
id  |      故事ID
title  | 标题    
lat  |    故事所在纬度
lng  |    故事所在经度
cover  |    故事封面图片  
distance  |    离搜索经纬度的距离(米) 
voice  |    故事语音链接
voiceTime  |    语音时长
voiceSize  |    语音大小
description | 故事描述

###故事作者

   参数名  |       描述 
-------- | ----------- 
name  | 作者名称    
avator  |    作者头像 
##地理位置搜索——景区景点
`https://api.fishsaying.com/geo-search/scenics?page={page}&limit={limit}&latitude={latitude}&longitude={longitude}&radius={radius}&type={type}&access_token={access_token}`

###HTTP方法
GET

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
latitude  |      double | 纬度       | 30.673916     | true
longitude  |      double | 经度       | 104.07318     | true
radius  |      int | 搜索半径(米) `1<= radius <=100,000`     | 10     | true
page  |      int | 第几页 `default:1, page >=1`      | 1        |   false
limit  |      int | 每页记录数 `default:10, 1<= limit <=100`  | 10     | false
access_token | string | 访问令牌 | 6e229bee-9cd8-4bf3-a610-8540672fc073 | true

###Response Example
```
{
  "total": 2,
  "page": 1,
  "size": 2,
  "data": [
    {
      "id": "00d8cd75e5d74d869e9d647069c8ab51",
      "title": "道安银花丝",
      "address": "四川省成都市青羊区草市街街道文殊院街15-17号文殊坊",
      "cover": "https://image-cdn.fishsaying.com/3d94b394481b236a6423ba81ea11.jpeg",
      "location": {
        "lat": 30.673916,
        "lng": 104.073185
      },
      "distance": 0,
      "type": 2,
      "description": "道安大师银花丝工作室原为成都道安艺术品有限责任公司，于2003年3月由道安创建，坐落在文殊院街15、17号。主要从事国家非物质文化遗产成都银花丝制作技艺保护传承工作，道安是国家级非物质文化遗产项目代表性传承人，中国民间十佳艺人之一，四川省工艺美术大师。"
    },
    {
      "id": "c5796ff6eb8d48ab86b530b4189a1fa4",
      "title": "致艺漆品",
      "address": "四川省成都市青羊区草市街街道文殊院街19号文殊坊",
      "cover": "https://image-cdn.fishsaying.com/89c15cfbf5b9d010c77359f24370.jpeg",
      "location": {
        "lat": 30.673923,
        "lng": 104.073175
      },
      "distance": 0,
      "type": 2,
      "description": "成都漆艺是我国最早的漆艺之一，现存于成都市青羊区。成都漆器又称卤漆，发轫于商周时期，金沙遗址出土的漆器残片现在依然文饰斑斓、色彩亮丽。到战国、秦汉时期，成都漆艺趋于兴盛，正如《史记》所言：“木器髹者千枚”、“漆千斗”。扬雄《蜀都赋》中亦称：“雕镂器，百伎千工。”在唐宋元明清几代，成都漆艺不断发展，对我国其他漆艺流派产生了较大影响。\n成都漆艺工序繁多、制作细致、耗时久长，尤以雕嵌填彩、雕填影花、雕锡丝光、拉刀针刻、隐花变涂等极富地域特色的修饰技艺闻名于世。成都漆器以天然生漆、实木为原料，胎体不拘，做工讲究,是集艺术性和实用性为一体的手工制品。它以精美华丽、富贵典雅、光泽细润、图彩绚丽著称，它既可高悬于庙堂之上以彰显华贵，又可充当精致耐用的日常用品。成都漆器既是历代习俗的重要见证和文化交流的使者，也是中国传统审美观念的重要载体。\n传统漆艺的手工性、艺术性决定了成都漆器不能采用工业方式生产，而只能通过手工劳动制出成品，同时也只能通过口传心授的方式传承。近年来，在传统与现代的夹缝中，成都漆艺正面临巨大的生存危机，产品市场狭小，制作者后继乏人，许多传统技艺已开始变形和失传，必须尽快采取必要的保护措施以挽救这种行将灭绝的古老手工艺。"
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
size  |   本次调用获取的故事数
###景区景点实体
   参数名  |       描述 
-------- | ----------- 
id  |      景区景点ID
title  | 景区景点标题
address | 景区景点详细地址
type  | 景区景点类型，1表示景区，2表示景点    
lat  |    景区景点所在纬度
lng  |    景区景点所在经度
cover  |    景区景点封面图片  
distance  |    离搜索经纬度的距离(米) 
description | 景区景点描述

##故事关键字搜索
`https://api.fishsaying.com/search/stories?keyword={keyword}&access_token={access_token}`
###HTTP方法
GET

###Request Parameters
   参数名称  |      参数类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
keyword  |      string | 关键字       | 诸葛亮     | true
page  |      int | 第几页 `default:1, page >=1`      | 1        |   false
limit  |      int | 每页记录数 `default:10, 1<= limit <=100`     | 1  | false
access_token | string | 访问令牌 | 6e229bee-9cd8-4bf3-a610-8540672fc073 | true

###Response Example
```
{
  "total": 1085,
  "page": 1,
  "size": 1,
  "data": [
    {
      "id": "65e84c22930941f68d0c7cf779b3cc53",
      "title": "诸葛亮 诸葛连弩",
      "location": {
        "lat": 34.262099,
        "lng": 107.626389
      },
      "cover": "https://image-cdn.fishsaying.com/6637e298bb2a4c5e8a0f4743254d02dc.jpg",
      "author": {
        "name": "qumumushi",
        "avator": "https://image-cdn.fishsaying.com/29b95c6cf1b04c9d9932093c6bd6544f.jpg"
      },
      "voice": "https://voice-cdn.fishsaying.com/964e50524fa14afa96abb252ff7ab855.mp3_trance_mp4?Expires=1487822347&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=213RnTdybYOnrLovnMdUnbfYe/4%3D",
      "voiceTime": 96,
      "voiceSize": 211566,
      "description": "陕西陕宝鸡市的岐山县有一座文化非常丰富的历史古庙，名叫五丈原诸葛亮庙。至今已经有了千百年了。五丈原诸葛亮庙有祭祀诸葛亮的宫殿。而说起诸葛亮呢，他可是千古智者的代表。他的一生就发明了不少的新玩意儿。其中就包括了用于战争的诸葛连弩。\n诸葛弩又称为诸葛连弩，是一种可以连续发射的弓箭，在当时是很厉害的武器，为诸葛亮根据旧有的技术所制成，一次可以发射十枝箭，大大提高了蜀军的战斗力。是诸葛亮发明的，又是可以连续发射的弓箭，而古代就称弓箭为”弩”,故以诸葛亮的姓氏命名为“诸葛连弩”。蜀兵虽少，却能六出祁山，逼进渭河平原，魏兵躲在深沟高垒上而不敢应战，又如建兴九年，魏将张合被蜀兵射杀，都可以证明诸葛连弩的功效。这连弩有两个基本数据，一是能连发十只箭，二是箭长只有八寸。中国人用弓箭是世界上最早的，欧洲人刚用弓箭的时候，中国人已经用了近千年了。而诸葛连弩是三国时期蜀国的诸葛亮创制的一种连弩,在当时十分先进，是现代军事武器的雏形，也是世界上最早的半自动武器!\n在五丈原诸葛亮庙来参观的时候，不妨多和身边的同伴交流诸葛亮的发明的故事，你也可以将诸葛亮发明诸葛连弩的故事讲给你的同伴听。相信大家都会有有新的收获。"
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
size  |   本次调用获取的故事数
###故事实体
   参数名  |       描述 
-------- | ----------- 
id  |      故事ID
title  | 标题    
lat  |    故事所在纬度
lng  |    故事所在经度
cover  |    故事封面图片  
voice  |    故事语音链接
voiceTime  |    语音时长
voiceSize  |    语音大小
description | 故事描述

###故事作者

   参数名  |       描述 
-------- | ----------- 
name  | 作者名称    
avator  |    作者头像 
##景区景点关键字搜索
`https://api.fishsaying.com/content/search?keyword={keyword}&access_token={access_token}`
###HTTP方法
GET

###Request Parameters
   参数名称  |      参数类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
keyword  |      string | 关键字       | 道安银花丝     | true
page  |      int | 第几页 `default:1, page >=1`      | 1        |   false
limit  |      int | 每页记录数 `default:10, 1<= limit <=100`   | 1     | false
access_token | string | 访问令牌 | 6e229bee-9cd8-4bf3-a610-8540672fc073 | true

###Response Example
```
{
  "total": 2,
  "page": 1,
  "size": 1,
  "data": [
    {
      "id": "00d8cd75e5d74d869e9d647069c8ab51",
      "title": "道安银花丝",
      "address": "四川省成都市青羊区草市街街道文殊院街15-17号文殊坊",
      "cover": "https://image-cdn.fishsaying.com/3d94b394481b236a6423ba81ea11.jpeg",
      "location": {
        "lat": 30.673916,
        "lng": 104.073185
      },
      "type": 2,
      "description": "道安大师银花丝工作室原为成都道安艺术品有限责任公司，于2003年3月由道安创建，坐落在文殊院街15、17号。主要从事国家非物质文化遗产成都银花丝制作技艺保护传承工作，道安是国家级非物质文化遗产项目代表性传承人，中国民间十佳艺人之一，四川省工艺美术大师。"
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
size  |   本次调用获取的故事数
###景区景点实体
   参数名  |       描述 
-------- | ----------- 
id  |      景区景点ID
title  | 景区景点标题
address | 景区详细地址
type  | 景区景点类型，1表示景区，2表示景点    
lat  |    景区景点所在纬度
lng  |    景区景点所在经度
cover  |    景区景点封面图片  
description | 景区景点描述
##历史人物关键字搜索
`https://api.fishsaying.com/search/figures?keyword={keyword}&access_token={access_token}`

###HTTP方法
GET

###Request Parameters
   参数名称  |      参数类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
keyword  |      string | 关键字       | 诸葛亮     | true
page  |      int | 第几页 `default:1, page >=1`      | 1        |   false
limit  |      int | 每页记录数 `default:10, 1<= limit <=100`   | 2     | false
access_token | string | 访问令牌 | 6e229bee-9cd8-4bf3-a610-8540672fc073 | true

###Response Example
```
{
  "total": 1,
  "page": 1,
  "size": 1,
  "data": [
    {
      "id": "54cf5bc89a0b8ab174545817",
      "name": "刘备",
      "start": "99999999",
      "end": "99999999",
      "ancients": [
        {
          "region": "亚洲",
          "dynasty": "三国"
        }
      ],
      "avatar": "https://image-cdn.fishsaying.com/FqeJQWoXu5xYCjZya_D0cEOeJLqt",
      "description": "",
      "nicknames": [
        "刘玄德"
      ]
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
size  |   本次调用获取的故事数
###历史人物实体
   参数名  |       描述 
-------- | ----------- 
id  |      历史人物ID
name  | 历史人物名
start | 出生年份，`99999999表示不详`
end | 逝世年份，`99999999表示不详`
region | 所在区域
dynasty | 所在朝代
avator  |    历史人物封面图片
description | 历史人物描述
nicknames | 其它称谓
##内容详情—故事
`https://api.fishsaying.com/articles/{id}?access_token={access_token}`

###HTTP方法
GET

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
id  |      string | 故事ID `path parameter`       | 569e37d37f9440933c8b6446     | true
access_token | string | 访问令牌 | 6e229bee-9cd8-4bf3-a610-8540672fc073 | true

```
{
  "id": "569e37d37f9440933c8b6446",
  "title": "罗平 生物群与三叠纪生物的接触",
  "location": {
    "lat": 24.884626,
    "lng": 104.308675
  },
  "cover": "https://image-cdn.fishsaying.com/FmwayQ57KWJkct35QBCFfwfcdVMw",
  "author": {
    "name": "拥抱不了",
    "avator": "https://image-cdn.fishsaying.com/FmfR6GQMjs1lNA5xLfsitwjLmxdU"
  },
  "voice": "https://voice-cdn.fishsaying.com/FpunapYvGUWZ9e6okGyhAF-4b-x0_trance_mp4?Expires=1487823461&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=AkcHxyoCmz%2Bq0Uk8v7zrMY7lXLo%3D",
  "voiceTime": 94,
  "voiceSize": 1490885,
  "description": "三叠纪是地质纪年的一个时期，在距今2.4亿年前，看起来是个遥不可及的时期，但是在云南省罗平县，却可以亲身体会到2.4亿年前的三叠纪，与三叠纪生物来一次亲密接触。\r\n在三叠纪的时候，罗平还只是一片汪洋大海，后来由于地质活动中的造山运动，罗平不断升高，海洋逐渐退出罗平，罗平就抬高为陆地，而那些三叠纪时期死亡的海洋生物的骸骨因为累积在海底的泥土之中，而在随着陆地的抬高过程之中也浮现出来了。于是如今罗平的山地之中就藏有大量的三叠纪的海洋生物，明显地暴露在山地表面，一眼就可以看到，而且这些海洋生物遗骸都是更具时间的早晚而累积的，在山地越高的地方的海洋生物是距今年代最近的，而越往下的则是越古老的生物，所以纵观这些海洋生物遗骸化石，就像是亲历了这些生物的进化历程。\r\n而除了山地上面暴露出来的生物群，在罗平的地层之中亦有着更加久远的海洋生物化石，越往下挖掘，生物的造型更加奇异，甚至还挖出过一个长得像龙一样小鱼化石，这可比看科幻片来得真实多了。看到罗平的这些远古的生物群化石，才会惊觉地球历史的久远，而有人类存在的历史只是沧海之中的一粟罢了。"
}

```
###Response Parameters
###故事实体
   参数名  |       描述 
-------- | ----------- 
id  |      故事ID
title  | 标题    
lat  |    故事所在纬度
lng  |    故事所在经度
cover  |    故事封面图片  
voice  |    故事语音链接
voiceTime  |    语音时长
voiceSize  |    语音大小
description | 故事描述
###故事作者

   参数名  |       描述 
-------- | ----------- 
name  | 作者名称    
avator  |    作者头像 
##内容详情—景区景点
`https://api.fishsaying.com/scenics/{id}?access_token={access_token}`

###HTTP方法
GET

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
id  |      string | 景区景点ID `path parameter`       | 54cdcb029a0b8ad439d02680     | true
access_token | string | 访问令牌 | 6e229bee-9cd8-4bf3-a610-8540672fc073 | true

```
{
  "id": "54cdcb029a0b8ad439d02680",
  "title": "武侯祠博物馆",
  "address": "中国四川省成都市武侯区武侯祠延熙大道 邮政编码: 610041",
  "cover": "https://image-cdn.fishsaying.com/FlLmuvycRipMO7HNpo16yst7Ky0J",
  "location": {
    "lat": 30.64604232978,
    "lng": 104.04794963963
  },
  "type": 1,
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
cover  |    景区景点封面图片
lat  |    故事所在纬度
lng  |    故事所在经度 
type  | 景区景点类型，1表示景区，2表示景点 
description | 景区描述

##内容详情—历史人物
`https://api.fishsaying.com/figures/{id}?access_token={access_token}`
###HTTP方法
GET

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
id  |      string | 历史人物ID `path parameter` | 54cf5bc89a0b8ab174545817     | true
access_token | string | 访问令牌 | 6e229bee-9cd8-4bf3-a610-8540672fc073 | true

```
{
  "id": "54cf5bc89a0b8ab174545817",
  "name": "刘备",
  "start": "99999999",
  "end": "99999999",
  "ancients": [
    {
      "region": "亚洲",
      "dynasty": "三国"
    }
  ],
  "avatar": "https://image-cdn.fishsaying.com/FqeJQWoXu5xYCjZya_D0cEOeJLqt",
  "description": "",
  "nicknames": [
    "刘玄德"
  ]
}

```
###Response Parameters
###历史人物实体
   参数名  |       描述 
-------- | ----------- 
id  |      历史人物ID
name  | 历史人物名
start | 出生年份，`99999999表示不详`
end | 逝世年份，`99999999表示不详`
region | 所在区域
dynasty | 所在朝代
avator  |    历史人物封面图片
description | 历史人物描述
nicknames | 其它称谓

##景区景点关联的故事列表
`https://api.fishsaying.com/scenics/{id}/stories?page={page}&limit={limit}&access_token={access_token}`

###HTTP方法
GET

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
id  |  string | 景区景点ID       | 54f424399a0b8afc44174e2c     | true
page  |      int | 第几页 `default:1, page >=1`      | 1        |   false
limit  |      int | 每页记录数 `default:10, 1<= limit <=100`     | 2     | false
access_token | string | 访问令牌 | 6e229bee-9cd8-4bf3-a610-8540672fc073 | true

###Response Example
```
{
  "total": 300,
  "page": 1,
  "size": 2,
  "data": [
    {
      "id": "53870bfb9a0b8a1c690a9e57",
      "title": "公元223年 惠陵与汉昭烈庙建成",
      "location": {
        "lat": 30.644555,
        "lng": 104.049381
      },
      "cover": "https://image-cdn.fishsaying.com/FrNyWoeM7fxkRLH1BC-6BTTQZ3yn",
      "author": {
        "name": "nvadia",
        "avator": "FuxmH20zaEqDRhnTSNnPoBnLdM82"
      },
      "voice": "https://voice-cdn.fishsaying.com/FgAGll2jrHa6a7d-XCdBg4YlqUZT_trance_mp4?Expires=1487831523&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=2o/fulBk8cw6//kjfoz8BgKYCxI%3D",
      "voiceTime": 247,
      "voiceSize": 540003,
      "description": ""
    },
    {
      "id": "53870d649a0b8a1869048ded",
      "title": "两晋南北朝 武侯祠的迁入与发展",
      "location": {
        "lat": 30.644555,
        "lng": 104.04938100000004
      },
      "cover": "https://image-cdn.fishsaying.com/FpiOdwlay25jWVZJXeeilkQzQT2j",
      "author": {
        "name": "nvadia",
        "avator": "FuxmH20zaEqDRhnTSNnPoBnLdM82"
      },
      "voice": "https://voice-cdn.fishsaying.com/FkV3nFuL0QgDnZI8JaKo-FARs3fr_trance_mp4?Expires=1487831523&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=KdzKr/BWYE2%2BOLFtlTi0%2BLHTEkQ%3D",
      "voiceTime": 162,
      "voiceSize": 356033,
      "description": ""
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
size  |   本次调用获取的故事数
###故事实体
   参数名  |       描述 
-------- | ----------- 
   参数名  |       描述 
-------- | ----------- 
id  |      故事ID
title  | 标题    
lat  |    故事所在纬度
lng  |    故事所在经度
cover  |    故事封面图片  
voice  |    故事语音链接
voiceTime  |    语音时长
voiceSize  |    语音大小
description | 故事描述

###故事作者

   参数名  |       描述 
-------- | ----------- 
name  | 作者名称    
avator  |    作者头像 

##历史人物关联的故事列表
`https://api.fishsaying.com/figures/{id}/stories?page={page}&limit={limit}&access_token={access_token}`

###HTTP方法
GET

###Request Parameters
   参数名  |      类型   | 描述 | 示例  | 是否必填
-------- | ----------- | ----------- | ---------- | --------
id  |  string | 历史人物ID       | 54cf5bc89a0b8ab174545817     | true
page  |      int | 第几页 `default:1, page >=1`      | 1        |   false
limit  |      int | 每页记录数 `default:10, 1<= limit <=100`     | 1     | false
access_token | string | 访问令牌 | 6e229bee-9cd8-4bf3-a610-8540672fc073 | true

###Response Example
```
{
  "total": 1248,
  "page": 1,
  "size": 1,
  "data": [
    {
      "id": "00494e75e58842608d079cfcfe849597",
      "title": "成语典故苑 长驱直入",
      "location": {
        "lat": 36.627336,
        "lng": 114.473793
      },
      "cover": "https://image-cdn.fishsaying.com/abdc7c43329c42b4a27d84c551484a08.jpg",
      "author": {
        "name": "川外130",
        "avator": "29b95c6cf1b04c9d9932093c6bd6544f.jpg"
      },
      "voice": "https://voice-cdn.fishsaying.com/920a2a57a38f4649b4d653b6c298ee23.mp3_trance_mp4?Expires=1487835647&OSSAccessKeyId=eVU7vlTYuZhtU21f&Signature=XsVe97cbwwK0cAq3C3TF3ww7ol0%3D",
      "voiceTime": 106,
      "voiceSize": 232959,
      "description": "成语典故苑 长驱直入"
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
size  |   本次调用获取的故事数
###故事实体
   参数名  |       描述 
-------- | ----------- 
id  |      故事ID
title  | 标题    
lat  |    故事所在纬度
lng  |    故事所在经度
cover  |    故事封面图片  
voice  |    故事语音链接
voiceTime  |    语音时长
voiceSize  |    语音大小
description | 故事描述

###故事作者

   参数名  |       描述 
-------- | ----------- 
name  | 作者名称    
avator  |    作者头像

