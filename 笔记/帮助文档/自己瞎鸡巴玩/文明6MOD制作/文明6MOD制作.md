# 基本知识

## MOD模组栏信息内容

![image-20220503140607262](F:\图像\typora图像保存位置\image-20220503140607262.png)

## 学习方法

初学所以要大量的 套用源文件来进行修改, 所以一定要多去源文件下 copy代码来学习 熟悉.

..\Sid Meier's Civilization VI\Base\Assets\Gameplay\Data目录下有本游戏 所有的 xml源码.   多去里面找.



# 构建一个单位

## 工具介绍

![image-20220503141306619](F:\图像\typora图像保存位置\image-20220503141306619.png)

![image-20220503141520296](F:\图像\typora图像保存位置\image-20220503141520296.png)

 各个文件代表的含义

## Unit_Gameplay.xml  参数设置

首先,我们找到 Units.xml源文件, 在里面 cp 我们要修改的代码.

### < types>标签

```xml
types标签里写了 本文件要修改哪些单位. 
<Types>
		type属性:对应了 游戏中的单位,这里我们可以自行原创, 只要功能对照着游戏内的单位来稍微改动就可以了. 基本所有的单位都以 UNIT为前缀  后缀为名字,看不懂英文 请活用谷歌翻译.
    	Kind属性:  固定格式
		<Row Type="UNIT_SUNLEI" Kind="KIND_UNIT"/>	比如这个就代表了一个 勇士单位.
</Types>


```

### < UnitAiInfos> 单位类型

一个单位可以拥有多个类型,一般为三个.

下面表格信息来源于谷歌翻译, 可能存在偏差

| 类型id         | 类型描述 |
| -------------- | -------- |
| UNITAI_COMBAT  | 战斗     |
| UNITAI_EXPLORE | 探索     |
| UNITTYPE_MELEE | 近战     |



```xml
<UnitAiInfos>
    UnitType属性: 单位名id,AiType:类型
    	<Row UnitType="UNIT_SUNLEI" AiType="UNITAI_COMBAT"/>
	    <Row UnitType="UNIT_SUNLEI" AiType="UNITAI_EXPLORE"/>
	    <Row UnitType="UNIT_SUNLEI" AiType="UNITTYPE_MELEE"/>
</UnitAiInfos>
```





### < UnitReplaces>  替换?

是否替换原有单位

```xml
	<UnitReplaces>
        CivUniqueUnitType:单位id , ReplacesUnitType: 要替换的单位id
        这个例子表明,用原创 孙雷 单位,替换游戏中的 勇士 单位
		<Row CivUniqueUnitType="UNIT_SUNLEI" ReplacesUnitType="UNIT_WARRIOR"/>

	</UnitReplaces>
```



### < typeTags>  兵种

| 兵种类型           | 描述     |
| ------------------ | -------- |
| CLASS_MELEE        | 近战     |
| CLASS_LANDCIVILIAN | 土地平民 |
|                    |          |



```xml
	<TypeTags>
		type:单位id,	Tags:兵种类型
		<Row Type="UNIT_SUNLEI" Tag="CLASS_MELEE"/>
	</TypeTags>
```





### < Uints>  **  核心数据

| 属性                  | 描述           | 数值类型                                                     |
| --------------------- | -------------- | ------------------------------------------------------------ |
| UnitType              | 单位id         | 存在此id即可                                                 |
| Cost                  | 花费的生产力   | int                                                          |
| Maintenance           | 维护费用       | int                                                          |
| BaseMoves             | 基本移动力     | int                                                          |
| BaseSightRange        | 视野范围       | int                                                          |
| ZoneOfControl         | 区域控制       | bool                                                         |
| Domain                | 海 空 陆单位   | DOMAIN_LAND(地)     \|\|    DOMAIN_SEA(海)      \|\|    DOMAIN_AIR(空) |
| Combat                | 近战攻击力     | int                                                          |
| RangedCombat          | 远战攻击力     | int                                                          |
| Ranged                | 远战范围       | int                                                          |
| FormationClass        | 编队类型       | "..."(默认)                                                  |
| PromotionClass        | 经验值升级路线 | "..."(默认)                                                  |
| AdvisorType           | 顾问提示类型   | "ADVISOR_CONQUEST"(顾问征服) 翻译有点让我不明所以            |
| Name                  | 单位名称       | "LOC_UNIT_XXXXX_XXXX"(文本ID)                                |
| Description           | 单位描述       | "LOC_UNIT_XXXXX_XXXX"(文本ID)                                |
| PurchaseYield         | 支付方式       | "YIELD_GOLD"(金币) \|\|   "YIELD_FAITH"(信仰)                |
| PrereqTech            | 生成科技需求   | "TECH_ARCHERY" (可能是科技id?)                               |
| MandatoryObsoleteTech | 淘汰科技需求   | "..."(默认)                                                  |
| TraitType(可选)       | 文明独有       | "..."(文明id)                                                |



```xml
<Uints>
	<Row UnitType="UNIT_WARRIOR" Cost="40" BaseMoves="2" BaseSightRange="2" 
         ZoneOfControl="true" Domain="DOMAIN_LAND" Combat="20"
         FormationClass="FORMATION_CLASS_LAND_COMBAT" PromotionClass="PROMOTION_CLASS_MELEE"
         AdvisorType="ADVISOR_CONQUEST" Name="LOC_UNIT_WARRIOR_NAME"
         Description="LOC_UNIT_WARRIOR_DESCRIPTION" PurchaseYield="YIELD_GOLD" 
         MandatoryObsoleteTech="TECH_GUNPOWDER"/>
</Uints>
```



## Unit_Text.xml  	设置文本

```xml
Tag: 文本id,   Language: 国际化 
<Row Tag="LOC_UNIT_PEON_DESCRIPTION" Language="en_US"> 英文
      <Text>A simple peon.</Text>	在这里编写文本
</Row>

<Row Tag="LOC_UNIT_PEON_DESCRIPTION" Language="zh_Hans_CN">  简体中文
      <Text>A simple peon.</Text>
</Row>
```





## Unit_icons.xml  设置ui

### UI对应位置

![image-20220503153512894](F:\图像\typora图像保存位置\image-20220503153512894.png)



可以使用自己原创的,也可以使用游戏自带的.    我们在   \Base\Assets\UI\Icons\Icons_Units.xml文件夹 可以找到 游戏原单位所使用的的  ui源码.



```xml
   **Name: 命名有规范  ICON_UNIT_XXXXX(图标id)  ||   ICON_UNID_XX_ PORTRAIT(头像id名)
	Atlas: 引入的icon画册,    
	Index: icon下标  注意  下标二字
<Row Name="ICON_UNIT_PEON_PORTRAIT" Atlas="ICON_ATLAS_UNIT_PORTRAITS" Index="1"/>
```







### 画册    

个人建议还是直接去扒拉源码方便,  或许以后我把所有画册都搞齐了 才会变方便.

#### ICON_ATLAS_UNITS 

图标画册,显示在单位的头顶上.

![image-20220503152510143](F:\图像\typora图像保存位置\image-20220503152510143.png)

#### ICON_ATLAS_UNIT_PORTRAITS

头像画册





## Units.artdef  模型

去  `\Base\ArtDefs\`  目录下扒拉源代码,  搜索对应的兵种单位

将`<Element>  </Element>`标签内的内容复制下来替换即可

![image-20220503181436894](F:\图像\typora图像保存位置\image-20220503181436894.png)



# 编译发布



基本都会自动适配的

### 