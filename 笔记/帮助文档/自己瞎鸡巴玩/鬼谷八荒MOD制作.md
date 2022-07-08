# 文件作用

## ItemProps.json(物品)

修改物品在背包中状态 

```json
 //东海明珠
    {
    "id": 857010,
    "name": "item_name85701001", //对应文本 json中的 key
    "type": 3,//5原料
    "className": 401,//508
    "hide": 0,
    "playerShow": 0,
    "npcShow": 0,
    "icon": "donghaimingzhu",
    "level": 5,
    "desc": "item_desc85701002",
    "isOverlay": 1,//0为可叠加
    "drop": 1,
    "dieDrop": 1,
    "auction": 1,
    "sale": 18500, //售价
    "worth": 37000 //买价
  },
```

## LocalText.json(文本)

描述文本 修改此文件可以 修改游戏内对应语句模块 所显示文本内容

```json
{
    "id": 125841,
    "key": "role_feature_postnatal_name12584", 
    "ch": "明珠有泪",
    "tc": "明珠有泪",
	"en": "明珠有泪"
  },{
    "id": 85701001,
    "key": "item_name85701001", //注意 key对应 ltemProps.json中的 name 属性
    "ch": "东海明珠",
    "tc": "东海明珠",
    "en": "东海明珠"
  },  
```

# TownRefine.json(合成)

```json
//合成真·鲤龙
   {
    "id": 315010,
    "level": 1,
    "name": "role_feature_postnatal_name31501001",
    "rewardID": 888315010,  //合成获得的成品
    "probability": 100,   //合成成功率
    "itemCostID": "5081195_10", //合成所需要的材料以及数量
    "moneyCost": 100  //合成需要的灵石手续费
  },
```

# TownMarketItem.json(永宁州商城出售)

```json

  // 出售东海明珠
  {
    "id": 5081195,
    "group": 3,
    "level": "1",
    "mainTown": 0,
    "conflict": -1,
    "amountMin": 1,
    "amountMax": 1,
    "weight": -1,
    "patch": 0
  },
//谷歌翻译
{
     “身份证”：5081195，
     “组”：3，
     “1级”，
     “主城”：0，
     “冲突”：-1，
     "amountMin": 10,
     “金额最大”：10，
     “重量”：-1，
     “补丁”：0
   },
```

# TownFactotySellArtifact.json(炼器谱售价)

```json
[
//炼器谱出售
  {
    "id": 1857010,
    "level": 1,
    "mainTown": 0
  },
]
```

# RoleCreateFeature.json(气运时长及出现概率)

```json
[
  {
    "id": 5418704,//04
    "type": 1,
    "group": 0,
    "level": 6,
    "duration": -1, //持续时间
    "refreshType": 0,
    "conceal": 0,
    "name": "role_feature_postnatal_name54187041",
    "effect": "54187041|54187042|54187043|54187044",
    "tips": "role_feature_postnatal_tips54187042",
    "iconAndDesc": "0",
    "lockLuck": 0,
    "introduceText": "role_feature_postnatal_intro54187043",
    "weight": 600   //先天气运出现概率
  }
 
]
```





# RoleEffect.json(气运属性)

```json
[
  {
    "id": 54187041,
    "effectType": 1,
    "value": "talent_1_200"  //悟性+200
  },
  {
    "id": 54187042,
    "effectType": 1,
    "value": "luck_1_200"   // 气运+200
  },
  {
    "id": 54187043,
    "effectType": 3,
    "value": "intoDungeon_54187041"
  },
  {
    "id": 54187044,
    "effectType": 3,
    "value": "moneyAdd_+2000"
  },
]
```

