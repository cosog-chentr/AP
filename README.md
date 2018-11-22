![油气生产敏捷计算分析系统](https://github.com/JinneePro/AP/blob/master/01.%E7%94%A8%E6%88%B7%E7%99%BB%E5%BD%95.png?raw=true)
## 一、产品简介
&emsp;&emsp;本系统主要在采集、控制的基础上，侧重油井全井的智能分析。系统应用大数据分析方法，对工况、产量、时率、平衡、能耗等生产关键指标进行统计分析，及时发现生产不正常井，挖掘生产潜力井，提升对目标区块和单井的管控能力。模块主要包括实时评价、全天评价、生产报表、图形查询。
## 二、 计算原理
### 1. 功图诊断
&emsp;&emsp;在数字功图的基础上，寻找特征点，根据特征数据，结合油井动静态数据进行综合诊断分析。识别的方法类似人脸识别技术，目前是前沿的功图诊断技术，诊断正确率接近100%，为井场预警和报警提供精准的数据支撑。  
- 8个点：最大载荷点、最小载荷点、最大位移点、最小位移点、游动凡尔打开点、游动凡尔关闭点、固定凡尔打开点、固定凡尔关闭点 
- 2条线：理论上载荷线、理论下载荷线
- 3个面积：功图封闭面积，功图与载荷轴、理论上下载荷线围成的2个封闭面积

|序号| 工况名称 |序号|     工况名称     |序号|   工况名称     |
|:--:|:--------:|:--:|:----------------:|:--:|:--------------:|
| 1  | 抽喷     | 11 | 油管漏           | 21 | 柱塞脱出工作筒 |
| 2  | 正常     | 12 | 游动凡尔漏失     | 22 | 杆断脱         |
| 3  | 充满不足 | 13 | 固定凡尔漏失     | 23 | 杆（泵）卡     |
| 4  | 供液不足 | 14 | 双凡尔漏失       | 24 | 轻微结蜡       |
| 5  | 供液极差 | 15 | 游动凡尔失灵     | 25 | 严重结蜡       |
| 6  | 抽空     | 16 | 固定凡尔失灵     | 26 | 轻微出砂       |
| 7  | 泵堵     | 17 | 双凡尔失灵       | 27 | 严重出砂       |
| 8  | 气锁     | 18 | 上死点别、碰     | 28 | 惯性载荷大     |
| 9  | 气影响   | 19 | 碰泵             | 29 | 应力超标       |
| 10 | 间隙漏   | 20 | 柱塞未下入工作筒 | 30 | 采集异常       |

#### 2.产量计算
&emsp;&emsp;应用地面示功图，计算阻尼系数，求解波动方程，消除地面功图的影响因素，得出井下泵功图，寻找特征点判断工况类型，根据不同工况应用不同分析方法计算单张功图产量，再结合生产时率计算日产量。  
&emsp;&emsp;单张功图产量=(有效冲程计算产量-间隙漏失量)/((1-fw/100)×Bo+fw/100)×净毛比  
>&emsp;式中：fw — 含水率；  
>&emsp;&emsp;&emsp;&emsp;Bo — 原油体积系数；  

![](https://mmbiz.qpic.cn/mmbiz_jpg/XWHaBYA7WIu7uEuFuMfzbNrphYGWaBPyJR7ASAHkV3VDXR7dJJusOsbYPujo0oEpNJh7eSRCE5ncz39hsOjCFA/0?wx_fmt=jpeg)  
#### 3.泵效
&emsp;&emsp;泵的实际排量与泵的理论排量之比的百分数称为泵效。泵的实际容积是一个定值，在生产过程中被以下五部分所占据：实际产液量、进泵气体量、泵的漏失量、冲程损失和泵内液体的体积变化影响。在实际计算中进行泵效分析，一方面可以在已知其中四个量时可求出另一个量；另一方面可求出泵内各个部分所占的比例，清楚地看到影响泵效的主要因素，从而采取相应的措施。  
（1）泵的理论排量  

```math
Q = 1440πD_p^2NS/4
```
式中：`$ Q $` — 泵的理论排量  
&emsp;&emsp;&emsp;`$ D_p $` — 泵径，m  
&emsp;&emsp;&emsp;`$ N $` — 冲次，1/min  
&emsp;&emsp;&emsp;`$ S $` — 冲程，m  
（2）泵效  
```math
η = Q/Q_p = η_1η_2η_3η_4
```
式中：`$ Q $` — 泵的理论排量  
&emsp;&emsp;&emsp;`$ Q_p $` — 泵实际排量  
&emsp;&emsp;&emsp;`$ η_1 $` — 冲程损失对泵效的影响，由泵功图求得  
&emsp;&emsp;&emsp;`$ η_2 $` — 泵的充满程度，由功图形状计算分析求得  
&emsp;&emsp;&emsp;`$ η_3 $` — 液体的漏失系数，考虑到泵工作时液体漏失的影响，包括间隙漏失、游动凡尔漏失、固定凡尔漏失  
&emsp;&emsp;&emsp;`$ η_4 $` — 体积变化影响，通过计算泵条件下的液体体积系数求得  
![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIswAmx7fgXdPngKJKqdibp9Kl2SWFPPa8tIYiaOaibE3sKYicoGvRJDJfGDGQibT2qj2Ol5CNtQ9xXIic5w/0?wx_fmt=png)
#### 4.杆柱应力
&emsp;&emsp;对一定条件下的抽油杆柱力学特性进行分析，建立相应的数学微分方程。当泵工作时，任意井深位置处，抽油杆柱的轴向负荷由以下几项组成：  
（1）抽油杆柱自重，作用方向垂直向下；  
（2）油井液体对抽油杆柱的液体静压力，其方向垂直于抽油杆柱轴线向上；  
（3）油管内液柱在抽油泵有效面积（即杆柱面积减去相连抽油杆截面积）上所产生的液体负荷，其方向垂直于柱塞表面向下；  
（4）油管外液柱对柱塞下表面的液体压力，其方向垂直于柱塞表面向上；  
（5）抽油杆柱与液柱运动所产水的惯性载荷。惯性载荷正比于悬点运动的加速度，方向相反；  
（6）抽油杆柱与液体运动所产生的振动负荷；  
（7）各运动之间的摩擦力，包括：柱塞与泵筒之间的摩擦力、抽油杆柱与油管之间的摩擦力、抽油杆柱与液柱之间的摩擦力等。  
&emsp;&emsp;根据杆柱组合，分析各级杆柱的受力情况，判断杆柱组合选择是否合理，应力百分比是最大应力与许用应力的百分比，当应力百分比超过100%，应力超标，建议及时更换抽油杆。图中分别为一级杆顶端应力百分比，二级杆顶端应力百分比。  
![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIswAmx7fgXdPngKJKqdibp9KqXeTC2hJz50y9XgfyUrP7gdPlxAJIbdwcicbkzRN1LMCtssPYibn7aicw/0?wx_fmt=png)
#### 5.系统效率
&emsp;&emsp;抽油机井的系统效率是指地面电能传递给井下液体，将液体举升到地面的有效做功能量与系统输入能量之比。即：抽油机井系统的水功率与输入功率之比。   
```math
η=η_s×η_d=P_r/P_i ×P_e/P_r =P_e/P_i
```
式中：`$ η $` — 系统效率  
&emsp;&emsp;&emsp;`$ η_s $` — 地面效率，指光杆提升液体和克服井下各种阻力所消耗的功率，可根据功图确定  
&emsp;&emsp;&emsp;`$ η_d $` — 井下效率，指抽油机的水功率与光杆功率的比值，井下部分的能量损失在盘根盒、抽油杆、抽油泵和管柱中  
&emsp;&emsp;&emsp;`$ P_r $` — 光杆功率，指光杆提升液体和克服井下各种阻力所消耗的功率，可根据功图确定  
&emsp;&emsp;&emsp;`$ P_i $` — 输入功率，指拖动抽油系统的电动机输入的有功功率  
&emsp;&emsp;&emsp;`$ P_e $` — 水功率，指将液体举升到地面的有效做功能量
#### 6.泵功图
&emsp;&emsp;泵功图中从上至下依次为一级杆顶端功图（地面功图）、各级杆顶端功图以及泵顶端功图（泵功图）。  
![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIvWf2DMx1F3zcMryfL8rpYgcnAia7D38VjsVz2e4VVw0wUNIUXN0wndAJdwTqzkn6MogC0N5thqqSg/0?wx_fmt=png)

#### 7.电参工况诊断
&emsp;&emsp;在日常生产中，电参数据能直接反应单井的运行状态、运行时率、能耗和紧急待处理工况。通过报警信息及时推送，实现由人员依赖型向设备依赖型、由处理问题滞后型向提前预警转变，提升决策响应速度，提高单井正常生产时率，保护机械设备，降低运行能耗。  
**（1）工况诊断**  
&emsp;&emsp;根据采集的单井电参数据结合计算模块内置的启抽定时器和人工智能确定的报警界限值，应用逻辑判断方法，智能诊断单井电参工况。  
&emsp;&emsp;启抽定时器：在油井启抽时，电流有可能超过界限值，如果这时候报警会产生误报，启抽定时器的作用是在启抽时避免误报。

|序号| 工况名称 |序号| 工况名称   |序号|    工况名称    |
|:--:|:--------:|:--:|:----------:|:--:|:--------------:|
| 1  | 正常     | 4  | 欠载       | 7  | 三相电压不均衡 |
| 2  | 缺相     | 5  | 过电压     | 8  | 三相电流不均衡 |
| 3  | 过载     | 6  | 欠电压     | 9  | 空             |
>工况为过载:**螺杆泵**对应**井卡**，**抽油机**对应**井卡**、**杆断脱**；

>工况为欠载:**螺杆泵**对应**杆断脱**、**皮带断**，抽油机对应**井卡**、**杆断脱**、**皮带断**；  

>三相电流不均衡:防止盗电。  

**（2）报警界限人工智能确定**  
&emsp;&emsp;不同单井生产状态存在一定差异，每口井的电流、电压等报警界限需根据实际生产情况确定；即使是一口井的三相电流、三相电压，每相的报警界限值都可能不一致。传统的人工确定方式工作量过大，合理值确定缺少依据，不能根据单井生产条件变化及时动态调整，严重影响诊断报警的正确性。  
&emsp;&emsp;针对上述现场应用实际问题，报警界限采用大数据人工智能确定功能，可以根据采集的单井电参累积数据，人工智能实时确定电流、电压等报警界限，无需手动输入，根据生产实际情况动态变化，降低误报，提高诊断报警正确率。  
![电流报警界限值](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WItgZOuA6Af2s4UMz3sk6p7F9dRIKxzOIKojmT6mNK3xSUGDToeduRtASelZ8C6s244zREiamq3M9bQ/0?wx_fmt=png)

#### 8.平衡度计算
功率（电流）平衡度=下冲程功率（电流）最大值 / 上冲程功率（电流）最大值  
![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIswAmx7fgXdPngKJKqdibp9KJJDjmTve2rzUBeCrk3HPR8DZzUg5C95NZibDTFibb3bLtoHCGacMBfIQ/0?wx_fmt=png)

### 二、实时评价、全天评价模块
#### 1.界面伸缩  
&emsp;&emsp;点击界面中的![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIvWf2DMx1F3zcMryfL8rpYgmpr5AfMlY3MzEaOic1SbmFHoCoQpjFyo91ofVxT0VuOtOqsZyiboDSew/0?wx_fmt=png)或![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIvWf2DMx1F3zcMryfL8rpYgZkwh3MIFbIsd1SqyKiatn2aM1wpujn8G7FmsQ43EsP2B57XbzAekQgw/0?wx_fmt=png)按钮可控制列表伸缩。  
#### 2.列表关联  
&emsp;&emsp;界面中统计图与统计表相关联，点击统计图中某一状态，列表中出现该状态的所有井信息。

![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WItgZOuA6Af2s4UMz3sk6p7Fias7nGAAUPFH52b5DjM51j9uF0gnw9vqwYzGeP8EMDaJEa9Z9G3ibhMw/0?wx_fmt=png)
#### 3.智能标签  
&emsp;&emsp;界面列表中鼠标悬停在某一单元格时将会弹出悬浮标签，如鼠标悬停在某井的电参工况上时，弹出的标签格式如图所示，代表当日第一条电参数据，格式内容为**2018年8月14日0点0分5秒 运行状态为运行，电参工况结果为正常，A/B/C三相电流为28.26/28.46/28.39，A/B/C三相电压为243.84/244.76/241.28**。如果电参工况发生变化，则会在后面追加一条新的电参数据。

![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIsgavNwDlfFAaicQNiaKVI0HwOTWvz9uiaa2no7whSM3GxH2o6iaic8vMFuTg50H1hkSeBtQaF7MUqmfqg/0?wx_fmt=png)
#### 4.数据刷新  
&emsp;&emsp;点击统计表下方![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIvWf2DMx1F3zcMryfL8rpYga4qD7Ucicq86Bn4prd22fmwN6VqiashiciatulReJjMibwmib4qo1Xpc7sOw/0?wx_fmt=png)图标，可对统计表中数据进行刷新。
#### 5.历史查询
&emsp;&emsp;在井名下拉框中选择或输入查询的井名，鼠标双击列表中某一行或点击查看历史按钮可以查询单井的历史数据，历史数据按采集时间的倒序显示，点击返回统计返回统计列表。

![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WItgZOuA6Af2s4UMz3sk6p7FtnOEjSQnkdL3iadMcMKp6WEFGoWXFprZibAGGiaGmRE3caKlnOlWsAfZQ/0?wx_fmt=png)
#### 6.曲线查询
&emsp;&emsp;点击右侧曲线按钮![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIvWf2DMx1F3zcMryfL8rpYg8C0QjYu7fjA8f51Z2MOAY9M1V7tev9ictFm8lpKA5rKdocnNkIlxNibg/0?wx_fmt=png)可查询各参数的历史趋势曲线，选择开始时间、结束时间可对不同时间段的曲线进行查询。

![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIvWf2DMx1F3zcMryfL8rpYgywI47PoeeqvLhP2ZG2e0Mn1ib86aETL8k9TocA8BDzeBHZMO81h6LNg/0?wx_fmt=png)
#### 7.图形导出
&emsp;&emsp;界面中所有图形均支持导出，点击图片右上角![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIvWf2DMx1F3zcMryfL8rpYgcV5aicjCMh0iaR4p3uqCJjicJClpwAOpulbqOAKfYmBibAfs464x9SHYicg/0?wx_fmt=png)按钮，可选择相应格式导出图片。

![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIvWf2DMx1F3zcMryfL8rpYgklUwPCbFYCH4cQoV2NKZt3BMICumjRafjnScu6X5eeEENmJfIK19vQ/0?wx_fmt=png)
#### 8.运行区间
&emsp;&emsp;全天停抽，运行区间为空；全天运行，运行区间为00:00-00:00；其他时间段表示在显示的区间段时运行。

![image](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIsgavNwDlfFAaicQNiaKVI0HwdX9LoUuJicAO6kdYTp0KN9cnia5fiaN0BKKIy5Rjd6k5ndJaoeicbXOPZg/0?wx_fmt=png)
#### 9.数据分析
&emsp;&emsp;分析、采集列表中的一组数据分别为加权平均值、最大值、最小值。

![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIsgavNwDlfFAaicQNiaKVI0HwXICibWeIhiaQhGF5Jica0Xd8AA1hc7nHJKKr8ZMtxn6s6ZABEico2XMSlA/0?wx_fmt=png)
### 三、组织、用户创建及权限分配
#### 10.单位管理
&emsp;&emsp;单位管理用于单位组织的创建、修改、删除，单位组织生成界面的组织导航。首先，点击创建按钮创建新单位，上级单位可选择已有各种单位，不选择直接创建根节点，选择对应的单位类别，点击保存生成新单位组织记录。

![image](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIsgavNwDlfFAaicQNiaKVI0Hwk4s0j8QlerHDmpVQzosysibZoia1SkhRsibFm0bggL4U7NJyDpdjM7JrQ/0?wx_fmt=png)
#### 11.用户管理
&emsp;&emsp;单位组织创建完成后，点击进入用户管理模块创建用户，点击创建按钮，创建用户信息。单位名称中选择已建的单位组织，**确定组织的用户登录后，只能看到该组织及该组织的下属单位对应的信息**。用户类型包括数据分析员（**具有数据查询权限**）、数据管理员（**具有数据查询、数据编辑、权限分配权限**）、系统管理员（**拥有最高权限**），用户名称（**不能重复**）、用户账号（**不能重复**）、用户密码可自定义，点击保存生成新用户。

![](https://mmbiz.qpic.cn/mmbiz_png/XWHaBYA7WIs4XnBKmBw7xjm0PF5MjXKslL9xHUAVE39QcNp8h5MSzfZXuBUQ1qUGV23TX1jyOIjZGttTQGOAsA/0?wx_fmt=png)
#### 12.权限分配
&emsp;&emsp;用户创建完成后，点击进入权限分配模块，为用户分配权限。首先给用户分配角色，选择单位组织，出现该组织下的用户列表，选中某一用户，给该用户选择角色，点击**确认**保存。接下来给角色分配模块访问权限，选择一角色，在模块列表中选择其可以访问的模块，点击**确认**保存。

### 四、数据配置
&emsp;&emsp;数据配置中各模块中的数据均可直接从Excel表中粘贴过来，也可导出至Excel。
#### 13.区块数据
&emsp;&emsp;区块数据中录入目前区块的整体参数（**一个区块一组数据即可**）。
#### 14.井名信息
&emsp;&emsp;16.井名信息模块中录入单井的基本数据。
>- 单位名称：单位维护模块中创建的单位名称;
>- 区块名称：区块数据中创建的区块名称;
>- 举升方式：抽油机、螺杆泵、电潜泵;
>- 设备地址：RTU的MAC地址，由10位数字组成;
>- 设备编号：一个RTU连接一口井填01，连接两口井填02......；
>- 功图采集间隔：功图采集的频率；
>- 时率来源：DI信号、电参计算、人工录入；
>- 视频路径：监控视频的URL路径；
>- 排序编号：井名在界面中显示的顺序。  

&emsp;&emsp;录入完成保存后如果需要修改井名，在待修改的井名处修改完成后点击右上角修改井名按钮保存。
#### 15.生产数据
&emsp;&emsp;生产数据模块中录入单井的生产数据。
>- 油压：未测油压数据可填写回压；
>- 泵级别：1、2、3； 
>- 泵径：28mm，32mm，38mm，44mm，51mm，57mm，63mm，70mm，83mm，95mm；
>- 杆级别：A，B，C，K，D，KD，HL，HY；
>- 杆内径：空心杆填写；
>- 杆长度：不考虑光杆、拉杆；
>- 锚定状态：包括锚定和未锚定；
>- 净毛比：用于产量标定，净毛比=实际产量/软件计算产量，默认值为1。
