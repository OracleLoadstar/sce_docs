---
sidebar_position: 2
---

# 如何使用 SCE API

:::info
此页面正在重建，部分功能可能没有写入
:::

### 1.1 SCE API 请求 & 响应格式

##### 1.1.1 获取支援卡列表

请求:
```bash
GET https://api.oraclestar.cn/api/umasce
Header:
{"x-api-key": "你的ApiKey"}
```

响应:

```json
{
  "source": "mongodb",  // 响应数据库
  "data": {
    "a1": "【0500·定刻通り】エイシンフラッシュ",
    "a2": "【1日の終わりに】スペシャルウィーク",
    "a3": "【2人のバウンス・シャッセ】キタサンブラック",
    "a4": "【43、8、1】ナカヤマフェスタ",
    "a5": "【7センチの先へ】エアシャカール",
    "a6": "【All'alba_vincerò!】テイエムオペラオー",
    "a7": "【Are_you_merry】エアグルーヴ",
    "a8": "【A_Win_Foreshadowed】シンボリクリスエス",
    "a9": "【Balliamo】ジェンティルドンナ",
    "a10": "【Ballroom_Tempest】ウオッカ",
    //...
    "anthor": "(BiliBili Wiki) https://wiki.biligame.com/umamusume/" // 数据来源
    }
}
```

##### 1.1.2 获取单个支援卡数据

```bash
GET https://api.oraclestar.cn/api/umasce?id=<id>
Header:
{"x-api-key": "你的ApiKey"}
```

响应:

```json
// 以 https://api.oraclestar.cn/api/umasce?id=a1 为例
{
  "source": "mongodb",
  "data": {
    "CardName": "【0500·定刻通り】エイシンフラッシュ",
    "Type": 0,
    "Rarity": "SR",
    "friendshipBonus": { // 友情加成 各等级段效果
      "Lv1": 10,
      "Lv5": 11,
      "Lv10": 12,
      "Lv15": 13,
      "Lv20": 15,
      "Lv25": 15,
      "Lv30": 16,
      "Lv35": 18,
      "Lv40": 20,
      "Lv45": 20
    },
    "moodEffect": { // 干劲加成 各等级段效果
      "Lv1": 10,
      "Lv5": 15,
      "Lv10": 29,
      "Lv15": 27,
      "Lv20": 33,
      "Lv25": 40,
      "Lv30": 42,
      "Lv35": 45,
      "Lv40": 47,
      "Lv45": 50
    },
    "traningEffect": { //训练加成
        // ...
    },
    "specialtyPriority": { //得意率
        //...
    },
    "initalFriendship": { // 初期羁绊
        //...
    },
    "speedBonus": { // 速度加成
        //...
    },
    "staminaBonus": { // 耐力加成
        //...
    },
    "powerBonus": { // 力量加成
        //...
    },
    "gutsBonus": { // 根性加成
        //...
    },
    "witBonus": { // 智力加成
        //...
    },
    "spBonus": { // SP加成
        //...
    },
    "eventRecovery": { // 事件回复
        //...
    },
    "eventEffectiveness": { // 事件效果
        //...
    },
    "failureProtection": { // 失败率下降
        //...
    },
    "costReduction": { // 体力消耗降低
        //...
    },
    "friendshipRecovery": { // 智力回复量提升
        //...
    },
    "EfriendshipBonus": { // 固有友情加成
        //...
    },
    "EmoodEffect": { // 固有干劲加成
        //...
    },
    "EtraningEffect": { // 固有训练加成 
        //...
    },
    "EspecialtyPriority": { // 固有得意率
        //...
    },
    "EinitalFriendship": { // 固有初始羁绊
        //...
    },
    "EspeedBonus": { // 固有速度
        //...
    },
    "EstaminaBonus": { // 固有耐力
        //...
    },
    "EpowerBonus": { // 固有力量
        //...
    },
    "EgutsBonus": { // 固有根性
        //...
    },
    "EwitBonus": { // 固有智力 
        //...
    },
    "EspBonus": { // 固有SP
        //...
    },
    "initalSpeed": { // 初始速度
        //...
    },
    "initalStamina": { // 初始耐力
        //...
    },
    "initalPower": { // 初始力量
        //...
    },
    "initalGuts": { // 初始根性
        //...
    },
    "initalWit": { // 初始智力
        //...
    },
    "anthor": "(BiliBili Wiki) https://wiki.biligame.com/umamusume/"
  }
}
```

### 1.2 错误响应 & 限制

##### 1.2.1 错误响应

|错误码|描述|样例|
|---|---|---|
|500|查询故障，例如服务不可用，查询参数错误|`HTTP 500: {"error":"所有数据库均无有效数据"}`|
|401|鉴权失败|`HTTP 401: {"error":"无效的API Key"}`|
|429|达到速率上限|`HTTP 429: {"error":"请求过于频繁，每分钟最多15次请求"}`|

##### 1.2.2 限制
目前我们已经执行了部分速率限制:

- RLM (Rate Limit Minute)

目前的RLM为15，即每分钟15次调用，如果您是开发者且有更多访问量的需求，你可以通过邮箱联系我们(oraclestar@oraclestar.cn)，或直接联系我们的项目运营(xingguangcuican666@foxmail.com)，我们会尽快为您处理。