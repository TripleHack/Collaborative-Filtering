# RecSys_Algorithm

信息过载，用户实际需求不明确；强依赖于用户行为。  

### Collaborative Filtering
#### item CF

给用户推荐他之前喜欢物品相似的物品  
电商场景下更看重实际转化  
信息流场景下更看重点击率  

$u(i)$表示对item i有行为的用户集合  
$u(j)$表示对item j有行为的用户集合  
分子部分表示user的重合程度，分母则是做了归一化  

$$s_{ij} = \frac {u(i)\cap u(j)} {\sqrt{|u(i)|\cup |u(j)|}}$$  
$$p_{uj} = \sum_{i\in N(u) \cap s(j,k)} {s_{ij} * r_{ui}}$$  
$r_{ui}$表示用户u对物品i的行为得分  
$s_{ij}$表示物品的相似度  
对user u进行item j推荐的得分是根据item i来计算的  
i 是 user u行为过的物品，并且取与item i最相似的k个item  
公式升级1：活跃用户应该被降低在相似度公式中的贡献度  
例如：某个电商系统，user a是批发商，买了很多物品，比如啤酒和书刊，但是不能反映他的兴趣，user b是普通用户，只买了啤酒和书刊，这可以反映他的兴趣。按照之前的公式，a与b的贡献度是一样的，我们需要降低user a的贡献度。  
公式2.1.3  
公式升级2：用户在不同时间对item的操作应给予时间衰减惩罚  
公式2.1.4  

#### user CF
给用户推荐相似兴趣用户感兴趣的物品  
如何评价相似兴趣用户集合  
找到集合用户感兴趣的而目标用户没行为过的item  
$$s_{uv} = \frac {N(u)\cap N(v)} {\sqrt{|N(u)|\cup |N(v)|}}$$  
$N(u)$表示用户u有过行为的item集合  
$N(v)$表示用户v有过行为的item集合  
分子部分是item的重合程度  
$$p_{ui} = \sum_{v\in s(u,k) \cap u(i)} {s_{uv} * r_{vi}}$$  
