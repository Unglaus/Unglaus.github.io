---
title: 绝密作战记录
tags:
- 作为日记加密
date: 2023-03-02 16:46:33
password: UPC
abstract: 与 Rhodes Island™ 取得弱神经连接时需要口令
message: 请输入与 Rhodes Island™ 取得弱神经连接时的口令：
wrong_pass_message: 与 Rhodes Island™ 效验口令失败，请重试。
wrong_hash_message: 与 Rhodes Island™ 效验口令失败，当前使用临时权限查看。
---

# 基础档案

【代号】Dr.Unglaus



# 每日记录

## 2023年

### 三月

#### 06 周一

今天本来是想试试Qt+VTK+PCL显示点云数据的，看了看如何QWeight提升为QVTKOpenGLNativeWidget然后使用，一直没实践，明天试试在Qt Designer里提升再编译，看看源代码怎么生成的，然后在学学怎么用来显示PCL点云

主要时间在试各种C++库在VS中配环境的办法，基本试出来了，明天整理整理些blog

就因为想写blog，又弄了弄hexo的配置，显示那个前端加密插件没发挥作用，搞了一会儿没搞出来，然后突然发现可以typora存图片到文章同名文件夹再发布上去，方便管理。不过在本地的图片相对路径是test/aaa.imag，而发布到hexo之后，它自动把文件夹合并了，md和img放在一起，所以发布到网上的图片的路径需要时aaa.img，相较于本地md文件中的路径少了前面的文件夹相对路径。为了让它上传时自动把路径改变，找了半天插件，最后找到hexo-asset-img这个插件可以实现我的要求，已加入收藏夹“hexo插件”中。

这样相比于传到图床上更安全，一方面本地图片都有各自的同文章名的文件夹，方便管理，上传到hexo的部分也都是md和img在一起，也很方便查看。

最关键的是我用github做图床时，本地加载不出来，网络上不挂梯子有时也看不了，很蛋疼，这样最好，最起码本地一定能看，不需要另外配一些东西。

#### 07 周二

今天上午稍微调了一下QVTKOpenGLNativeWidget在Qt中的配置，在Qt Designer中拖动QWeight并将其提升为QVTKOpenGLNativeWidget，然后编译，看源代码的生成。其中有一点要注意，需要将VS属性中Qt setting的model部分勾选QVTKOpenGL，因为QVTKOpenGLNativeWidget是继承自QVTKOpenGL的，不然会有错误，具体见blog。然后被向阳叫去帮他看程序，帮他配了一下Qt新窗口同Qt Designer绑定。再然后被拉去打扫实验室卫生，隔三差五打扫卫生。。。随便弄弄又到饭点了，一上午草草结束。

下午摸鱼摸到4点，摸到方舟怪猎联动开服，抽了抽卡，打了会儿关卡，感觉也没干什么就到5点了，然后又被向阳叫去帮他看程序，关键看了半天也没解决，晚上还有课，昨天说要写的blog还是没写，又要拖到第二天了，就感觉一天了自己的事儿一点没弄，搞得很烦躁。

晚上就是上课，算法分析与设计，不知所云，纯坐牢。下课九点半，回宿舍洗洗澡，玩玩密特罗德：生存恐惧，结果又迷了一晚上路，最后发现是因为新地图有条路被隐藏砖挡住了，这个隐藏砖需要变成球放的紫色炸弹才能打开，一开始没找到导致我把所有图几乎又跑了一遍，等找到这条路都11点半了。（这条是第二天回工位写的，不然一般记录是在工位写完回宿舍玩去了，晚上的游戏记录一般不会写）

#### 08 周三 

上午又帮向阳看了看程序，最后还是搞不定，这东西我需要自己花一段时间学，没学过直接给我叫过去看半天我也弄不来啊，弄到大概10点放弃了。然后写了会OCC+VS配置的blog，稍微去4楼干了点活，结束

下午过来坐着想把那些教程blog都补上，林波师兄过来问PCL初始显示点云的时候默认追踪点云显示，我也不会啊，稍微看了看，没找到相关代码。然后贾老师又让去统计小组要买的白大褂的尺码，去找业茹师姐要了购物链接，然后看了看，做个excel，也没弄什么半天过去了，再一看时间已经4点半了，这周还啥也没干呢。。。

晚上一直在写OCC+VS安装及配置，没想到写了那么久，到最后也没写完，还差一点

#### 09 周四

把昨晚差的哪一点小教程写完，结果没想到写完11点了，一上午基本过去了，这周组会讲啥啊。。。

下午，干了什么来着。。。

晚上在看CloudCompare Wiki学习一下软件的使用，然后又自己试了试，大部分时间摸鱼玩方舟去了。。。

然后想着把Qt配合VTK显示点云给弄出来，结果遇到一堆问题，弄半天弄到11点了，服了，明天早上稍微试一下，还不行就随便做个ppt，汇报完再弄吧

#### 10 周五

弄了一上午，没有什么结果，具体去看blog，不过基本确定了，应该就是两个vtk版本都放一块可能有点冲突，还是要吧自己编译的vtk9.2覆盖掉pcl自带的vtk9.1，然后重新编译一下pcl，这样应该就没问题了。不过因为要开会来不及了，所以先把ppt做了，这个重新编译pcl之后再试吧

2点跟杜二宝师兄开了个会，确认了一下当前开发点云处理软件的配置，杜师兄说就在windows下弄就行。另外，说我那个圆柱点云拟合出来的数据肯定不行，再查查论坛啥的看看别人怎么弄的。

开完组会之后就啥也不想干了，到点收拾收拾走人了，晚上跟欢儿打了打乒乓球，欢儿兵乓球有一手的。

#### 11 周六

跟毅他们约着出来玩。

<span style="background:#000000;color:black" >本来约的下午一点半，结果某强愣是睡过头，最后下午五点才来。</span>

打麻将打到9点，回学校10点半，玩了玩睡了

#### 12 周日

密特罗德：生存恐惧通关，又花了2小时左右全收集了一下，然后打了打boss rush模式，好玩的这游戏。不过就买个二手卡带玩玩，玩完再出了就好，毕竟300+的话，感觉还是。。。



#### 13 周一

尝试一下用自己编译的vtk9.2配合pcl自带的其他3rdpart重新编译pcl1.12.1

编译PCL的时候照着别人的教程设置了pcl_find_boost.cmake，手动添加了boost 的include和lib位置，结果还是cmake的时候还是找不到boost的位置。最后发现是因为文件夹路径中含有空格“pcl 1.12.1”导致的问题，将路径中含有空格的文件夹名称更改，去掉空格之后，cmake的时候就能顺利找到boost 了

我又试了一下，果然就是因为路径里文件夹名字有空格，它就会找不到路径，把空格删掉就能正常找到路径

之后就是正常编译PCL，然后稍微改了下环境配置，再跑一下代码，果然没有问题，搞定，写写blog收个尾。

#### 14 周二

昨天关于PCL配置的blog没写完，争取上午写完

惊了，写了一上午加一下午还没写完，效率太低了。。。摸鱼摸得有点过了。。。

晚上又要去上听不懂的课，上完回宿舍玩去了。。。

主要写教程的时候因为我安装过了，有些图不太好搞，我又不想把配好的东西删了重新配，配图片画的时间多了点。。。

考虑要不要先文字描述，然后把图片位置流出来，等在新电脑配的时候再截图。也不是不行。

#### 15 周三

上午。。。上午好像没干嘛，有印象的就是把PCL配置那个教程又写了写，但还是没写完。

下午试了试OCC+Qt读取Step文件，一开始总是报错，最后发现，其实是因为文件读取路径用了反斜杠，导致文件没有读出来（**突然认识到，读文件时加一句if判断，如果文件为空，弹出提示这种语句的重要性了**），文件路径的反斜杠改成斜杠就行了。以后记得在读完文件之后，后续要执行的语句外加一个if判断，判断该文件不为空再执行，若为空返回个提示。这样也不至于卡半天了。。。

然后突然对OCC的Qt例程中使用myObject3d.Append()这种方式显示模型的方式感兴趣了，也学了一点点Qt，这次再去试试能不能看懂。

结果晚上睡着了，醒了8点半，写了写PyCharm缓存移到别的位置，就结束了

#### 16 周四 

看了看Qt程序的执行过程，把它的项目文件结构搞明白了，然后写了个blog总结了一下

晚上学了学vue，他官网给了个互动教程，感觉不错，把常用的组件以及简写都说了一下，就比如它常用的Attribute绑定，`v-bind`指令，拿`div`举例`<div v-bind:id="dynamicID"></div>`，其中的`v-bind`一简写，就变成了`<div :id="dynamicID"></div>`，就剩个冒号了，这一般还真不知道是个什么意思，也没法查起。还有事件监听，`v-on`指令，拿`button`举例`<button v-on:click="increment">{{ count }}</button>`，可以简写为`<button @click="increment">{{ count }}</button>`，这种@的写法我感觉还真见过不少，当时没学不知道是什么意思，原来是事件监听`v-on`的缩写

然后写了写周五上午和下午两个组会的ppt干到11点，一天又结束力。

明天开一天会估计也不想干什么，回首这周感觉啥也没干啊。。。

明天干脆把blog补一补收工算了。。。这能毕业吗。。。

#### 17 周五

上午开完，下午开，开完啥也不想干

<span style="background:#000000;color:black" >晚上还被PUA，叫我去玩，我不想去，结果都不去了？什么鬼啊</span>

<span style="background:#000000;color:black" >还有班里组织个活动，也不先统计个人数，直接搞了个2500的别墅，去的人少直接资金爆炸，还来催人，催过来催过去，差不多得了</span>



#### 18 周六

<span style="background:#000000;color:black" >班长又来催，我真服了，我TM考虑呢，你这催什么呢我真服了，给我催烦了，想去也不去了。</span>

上午弟弟来考奥赛，带着逛了逛学校，吃了个午饭

<span style="background:#000000;color:black" >然后给他拍图书馆照片的时候，直接一坨鸟屎拉头上了，wtf？</span>

<span style="background:#000000;color:black" >回来洗个头，洗发水瓶子又摔坏了？</span>

<span style="background:#000000;color:black" >不给班长面子还被诅咒了？快去破财消个灾吧，真服了，这下是真的晦气了。以后不敢整天乱说了。</span>

<span style="background:#000000;color:black" >等玩完看看写个感谢。看看这保底200+大洋花的值不值感觉</span>

---

<span style="background:#000000;color:black" >回来了，我的评价是，不如氪金</span>

<span style="background:#000000;color:black" >想说点什么，又觉得不能说太死，总之就是，不予置评。</span>

<span style="background:#000000;color:black" >等看看每个人分多少钱，就当丢了吧。</span>

---

<span style="background:#000000;color:black" >钱算出来了，258，血亏</span>



#### 20 周一

课题组给配的电脑来了，开始在新电脑上安装需要用的软件。

不过在安新软件之前我发现当时win11激活时直接用的微软账号，所以C盘用户文件夹的名字直接是我的邮箱前5位，很难看，然后我去查怎么安全的改这个名去了，就这估计搞了一上午，下午才开始安各种软件。

安到hexo的时候在想，怎么让两台电脑的hexo博客同步啊，然后去查，然后照着配置，结果配完之后在测试的时候发现git pull的时候本地文件没更新。然后一直在尝试，试到晚上都没试出来，卡住了。

#### 21 周二

安了安其他软件，然后又去搞昨天卡住的hexo多设备同步问题去了，之前只是照着配，这天去看了看具体的原理之类的东西。

下午两点去搬东西，弄完回到工位三点半了好像。

然后下午又想试一试昨天git pull那个问题的时候，发现在原电脑git push的时候出错了。然后也没弄了，晚上上课去了。

#### 22 周三

上午查了查之前git push出的错，然后又测试了一下git pull，发现成了，之后两台电脑都测试了一下。可以互相git push 和git pull了，也就说终于配置好了，之后就不怕在工位写的blog和宿舍写的blog冲突了。

可以开始愉快的更新blog了，准备把更几个blog，这次hexo多设备同步的步骤更一个，更改win11用户文件夹名字更一个，再稍微弄个小的git笔记？

然后一下午把之前旧电脑上的项目git到GitHub上。晚上试试pull到新电脑上

在pull的时候基本上很顺利，通过这种方式比u盘直接拷贝快不少，当然前期准备也复杂一点。

但是还是遇到了问题，pull下来的项目中，与qt有关的项目都找不到头文件位置，可能是因为qt安装的位置不太一样，加上qt的小版本也不太一样，他现在只有在线安装包，当时安的时候是6.4.0，过了几个月？就变成6.4.3，之后都没有6.4.0的安装包了，这我咋办。。。

找了找vs里qt可能的环境配置的位置，找不到，搞不懂，想了想干脆在新电脑上把Qt有关的项目重新建一遍，然后把pull下来的代码复制上去。之后如果想搞同步的话，把旧电脑原来的qt6卸载，安装到跟新电脑一样的位置，反正得保证至少有一边是能用的。其实如果两个电脑qt安装的位置一样的话，可以试试把旧电脑上的qt用它自带的安装包更新一下试试。

然后因为是vs+qt创建的项目，所以可能还要注意一下qt vs tools的版本？

<span style="background:#000000;color:black" >话说今天电梯的见到一个长得对胃口的妹子，但是男朋友就在旁边。突然就有点emo，像这类女生都有对象了吗，到现在了都多久没谈过对象了，是不越往后找到没谈过的几率也少了，或者说剩下的没谈过的会不会都是我看不上的那种？或者说以后找的对象她有好几个前任，接受的了吗？就想想就感觉是不是要抓点紧了？但想了想又不知道从何下手，一是看到有感觉的妹子感觉几率不大，主要是自己参加的活动太少，但你说看见了吧，也是像今天这种路上遇到，今天这个旁边有对象，但就是没对象我也不太可能上去跟人家搭话。。。这种感觉好像就是上次班里轰趴给加重了，就看着那些女生我就感觉。。。周围只有这种的了吗。。。可能加深了这种焦虑，感觉完全没有我的菜。。。好姑娘可能都无了，以后就算有可能也都有过前任经验，而不是完完全全属于我的那种的感觉。。。精神洁癖？寄。。。以后难道只能靠相亲找个没有感情的，然后两个人搭伙过日子这样了吗。。。好惨一男的。。。</span>



#### 23 周四

<span style="background:#000000;color:black">晚起的人有漂亮妹子看。</span>

昨天晚上把Qt相关的工程在新电脑重建了一下，也没干什么好像，但就是待到挺晚，回宿舍都12点了，睡觉的时候快一点了，不能再这样了，不然早起真顶不住，而且老睡这么晚身体不行，脸上都疯狂爆痘了。

今天在床上墨迹到8点半才下，出发去工位都九点了。<span style="background:#000000;color:black">不过今天在电梯间又看到了漂亮妹子，对胃口的那种，不知道有无对象，就假定没有，稍微缓解了一下昨天晚上的焦虑，看见漂亮妹子就是开心。</span>

<span style="background:#000000;color:black">突然想到，之前那种焦虑，也有很大一部分原因可能是B站刷到的那类相亲奇葩视频搞得，看这些牛马看多了，就感觉没正常人了，真服了，就看那些傻卵东西看的，导致我觉得自己对妹子心态都不正常了。</span>

重要结论：没事少看B站。<span style="background:#000000;color:black">现在B站也就是新型垃圾场，什么负面垃圾新闻到处是，看多了人能好就怪了。尤其那些相亲相关视频，净把些狗屎拿出来讲，来恶心人。</span>



#### 24 周五

昨天写完那个PCL+QT+VTK编译的blog写到晚上12点。。。就在想是不有点浪费时间了，做这个有意义吗。。。陷入沉思

感觉还是不要花太多精力，主要还是记记学习笔记吧，这种配置环境的教程还是有点花时间。。。要不就以后配置的时候边配边写？应该能省一点时间？反正自己平衡一下吧。。。

汇报完ppt收工



#### 27 周一

上午看了看科技前沿，chatGPT4和各大公司的联合应用，有微软的office 365 copilot和GitHub的copilot ，然后看了看GitHub copilot能干的事，面向注释的编程，想搞一个玩玩，发现可以GitHub学生认证免费用，在这弄GitHub学生认证，一直通不过，有点烦。最后试试把学信网报告转英文看看有用吗。

上午一直到最后也没过，用电脑上传jpg截图就是不得行。

下午一来用手机来认证，直接页面上选拍照，拍了个学生证，直接秒过，惊了。。。总之，最后结果是好的。。。

看了看大礼包送的东西，都不大认识。。。常用的反正就是JetBrains大礼包，每年都要续一下；然后可以免费用Github copilot了；还提供了6个月的Educative，可以上去看课，想想不错，等着可以去看看；还有微软的Azure云平台可以用，好像是用来跑人工智能的，有空可以去看看；再就是提供了一年免费域名给用，感觉暂时不是刚需，没仔细看。。。

听说过两年要重新认证一下，看到时候能记得吗。。。

稍微配了一下VS+GitHub copilot试了试，感觉就那样。。。可能现在写代码还是少了，用不上这么牛的功能。。。反正也就是个辅助功能，还是要提升自己的编程能力，多动手写点代码。

晚上看了会儿cloudcompare文档



#### 28 周二

上午，下午看了会儿cloudcompare文档，然后被叫去给实验室激活电脑，以后记得win11用新账号注册登录的时候出生日期一定要选个大于18岁的日期，不然一堆屁事。

今晚去上算法课，最后出了两个小算法题，让用分治的思想做一下并分析算法时间复杂度。一个是让给定一个序列（有正有负），让求其中最大序列段，若有多个相同大小的序列段，取最短的那个；第二个是给定一个序列，求里面的所有“逆序对”。感觉都不是什么很难的题，但是就是毫无思路，作为一个计算机人（自认），感觉很受打击，跟毕业那会儿一个样，虽然上了研究生，但这方面还是毫无进展，啥也没学会啊，让当时我们本科的大佬来写估计分分钟搞定，都懒得看的题。。。感觉还是要花些时间搞搞这些基础算法的思想，虽然这个算法可能用不大上，但这个过程中锻炼的思维我感觉还是很有用的。你学计算机你不把算法学好你也配自认计算机人？

另外分析算法时间复杂度的“大师法“？是个什么来着，之前讲过，没仔细听，记得去研究一下。

#### 29 周三

看了会儿cloudcompare文档，9.30去四楼实验室，有领导来考察，上午基本没干什么

下午看了会儿文档，也没看多少。

晚上去跑了个步，洗了个澡，放松了一下。

#### 30 周四

又看了会儿cloudcompare文档，觉得就是讲了讲软件怎么用，对实际编程感觉没什么大用，就没再细看，不过对软件基本功能有了个大致了解，但具体使用可能还得多用用试试。

然后根据前几天看的cloudcompare的文件结构，找了找界面显示相关的源码来看。

下午刚看了一会儿？其实还没开始看，刚来没一会就又叫下面干活去了，干到6点半，有啥也没干结束了。

明天又两个汇报，晚上做做ppt，一周又啥也没干结束了。。。

#### 31 周五

上午，组会+写会议纪要

看了看正版项目任务书，今年5月-10月，按计划书上我要写出点云滤波和压缩的算法设计方案，并申请一份软著？<span style="background:#000000;color:black" >wtf？这不早点让我知道？</span>

做吧，加把劲做吧。。。



### 四月



#### 03 周一

今天8点闹钟看了眼，想再眯一会儿，再一睁眼以为顶多8.30，结果一看9.30 。。。哈哈，干脆上午在宿舍学一会儿，下午再去吧。。。

在宿舍不用担心被叫去干<span style="background:#000000;color:black" >jb</span>杂活，爽哎！

下午3点去四楼实验室打扫了下卫生，4点多搞定，也没学，玩了会儿5点半吃饭去了。

晚上不想去了，想着在宿舍学会儿，结果看了集“天国大魔境”的动漫，忍不住去补漫画，直接看到10点。。。正好欢儿过来打游戏，无缝切换大乱斗。。。



#### 04 周二

下雨阴天，不想去工位了，在宿舍学了学八叉树的概念和原理

结果就把八叉树相关的知识点看了看，大概搞懂了它的存储原理和结构，但具体实现，如何对具体的点云数据用八叉树分割存储还是没太懂，需要再研究一下

晚上上了个课，洗了洗澡，结束了



#### 05 周三

清明节，听说放假，又是不去工位的一天，本来没打算真休息，想着看一眼火纹engage新更新的dlc邪龙之章，结果更新要40min（手机热点更新）。正好昨晚抽风打开了奥日2玩了一点，寻思等更新的时候玩一会儿吧，结果这一玩直接上头玩到通关，一直玩到晚上12点半。不过玩的时候也感觉，不如一代好玩，关卡设计可能为了受众降低了难度，关卡长度感觉也短了，打完之后没有一代那种酣畅淋漓的快感。也可能是连着玩玩麻了？不对，一代我也是一天通过的，但那个玩完就很爽感觉，这代反而有地方迷路，技能太多忘了用哪个能过去新场景导致过程有点折磨。这么想来一代通关时间9.9h，二代13.4h，但是一代大部分时间花在那几大关卡点上，花在不断尝试通关过程上，最后通关很爽；而这代时间相比一代其实游玩时间大多浪费在找路上了（扩充了地图？有很多地方能看出借鉴了空洞骑士，比如还有卖地图的之类的。。。），而那几个大关卡试了没几次，没花多久就过了（毕竟关卡长度也短了），就没有那种畅快感，就一直跑流程在那。。。

总之，回想起来一代精简明快，一个核心技能从头爽到尾；二代技能臃肿，缺乏引导，有时候不知道到哪该用哪个，导致卡关迷路，不爽。

不过游戏质量还是不错的，只是跟一代比感觉还是一代好玩。。。

惊了，怎么还写起测评来了。。。



#### 06 周四

今天试了试用Cmake编译CloudCompare源码，又安了一下Qt5.15.2的版本，编译出来看了看

之后写了写编译笔记，然后？忘了干什么了就结束了。。。

今天好像被传染了，有点不舒服。



#### 07 周五

做ppt有感，好像做ppt的时候学习效率还高点？就是为了做ppt有东西讲，看东西的时候会比较集中，动脑也多一点？以后试试周一开始就按做ppt的态度来学习？边学边做ppt试试？



#### 08 周六

不知道刮得什么风，妹妹找我吃饭，去尝试了下日料。吃不来，还贵。吃饭的时候老师突然通知来活了。

#### 09 周日

上午师兄开了个会说了说活什么做，听完还是不会做

墨迹到下午，叫回家吃了个饭，螃蟹真不错，<span style="background:#000000;color:black" >尝了尝茅台，确实很柔和，一点不辣</span>

活儿是一点没做

#### 10 周一

下午六点前要交了，赶紧做了做，虽然卡点交了，但感觉做的不大行。主要还是没啥头绪，没个范例，写完也有种挫败感，因为看了看师兄们写的，觉得自己这东西写的更不得行了，但也没时间改了，其实就算让我改我感觉也不知道怎么改。。。就是没啥头绪

中午写着的时候咸鱼还来个奇葩，问这问那，又给他拍视频又回答他问题，屁事不少，关键屁事都问完才问最低价多少？我tm给你问这么半天你要是嫌价格有问题不要了我不是白忙活，就不能先问问价格？幸好是说行，也下单了，准备下午交完稿给他发，结果过了1个小时左右过来问我质量问题能退货吗？wtf？我是二手卖家，又不是商家，卖出去之后还管售后？真到时候坏了我可不知道你怎么弄坏的。而且你不是要发票什么的吗，你自己去保修啊，我商品描述页也写了不支持退货，你还在这问，当时就无语了。然后跟他说完不支持，直接不要了，申请退款，我真无大语，瞬间同意并拉黑了，别再来浪费爷的时间了，惊了，忙着呢。。。

晚上了，明天还有个ppt要交，看着做一点。

回宿舍的路上还是没忍住，找了那个1450的主，这次咱找的人家，也不好提不包邮了，就寻思赶紧卖出去得了，当时就听涵宝的建议直接跟他谈不包邮1450就好了，最起码能省个邮费钱说不定。这几天来看，问的这些人都直接往1400砍，也不知道跟谁学的都，也不敢降价到1500了，到时候再冲过来一堆傻卵给你往1300砍怎么办，1450卖了就卖了吧，小亏一些，耳机放我手上也不怎么用，到时候时间长了卖不出去估计更卖不上价钱去了，感觉卖出去省的老是想着个心事，再一个也不用再有上午那种二傻子过来骚扰我了。

那人倒也痛快，一问要不要直接就要了，也没问这问那，希望到时候收货，收货后也没什么问题。

#### 11 周二

上午做了做ppt，还是没啥头绪，感觉做的不好，弄得心情也不太好，去发个货，回宿舍歇了。

顺丰到底是贵，23元的运费，不过包装也确实好，最起码寄过去应该没什么问题。坑爹的是之前赔偿我的那个顺丰那个钱，还剩8块，不可以不够的的从微信出，必须充值才行，但最低冲30元，这不有病吗，现在最低估计邮费也没有8块的了，这8块就当扔里面了，纯恶心人。

这样的话，1450-23=1427，静回血1427元，买的时候1709元，1709-1427=282，从买到现在也快半年了，就当花了282元体验了体验高端耳机吧。



#### 12 周三

昨天晚上吃的那顿饭不知道怎么了，一直没消化了，晚上在床上躺着难受到2.30也没睡着，下去吐了吐，感觉是一点没消化，基本全吐出来了，还能好受一点了。3点回床上躺着慢慢就睡着了。

7、8点钟醒了，但不太舒服，不想起，墨迹到11点，去餐厅喝个小米粥吃个南瓜养养胃

中午手脚发凉，感觉有点冷，回床上躺着，感觉可能有点小烧，下次睁眼发现下午5点了，晚上去喝了个南瓜粥，吃了个地瓜，感觉舒服点了 

不过头有点痛，可能之前真发了点烧，不过现在摸摸头也不热，应该是过去了

今天一天都在宿舍歇了。



#### 13 周四

上午多睡了会，养养病。然后上了节辩证法的课。

下午去工位稍微学了会儿。

晚上开班会，开晚班会做了半小时ppt，马上被叫去干杂活，干到10：30

回宿舍洗了个澡，跟阳阳交流了一下。

打工人，相互理解，别那么多怨言，干就完了，日子会越来越好

不过我感觉我对帮课题组干活其实没什么怨言，<span style="background:#000000;color:black" >我就是不爽马x老是叫带着我们小组的人薅，真就逮着老实人欺负是吧，有病</span>

另外，耳机成功收货了，确实痛快，今天上午到的货，9点签收的（估计刚下班），11点确认收货的。1450到账（实际回血1427），好耶。



#### 14 周五

上午PPT汇报

下午PPT汇报

汇报完之后啥也不想干

下午汇报完直接跟兄弟们出去吃饭了，吃完8点了，直接回家去了，回去看看家人。



#### 15 - 16 周末

回家看了看爷爷奶奶

在家看了看买的漫画，虽然看的是漫画但看书的过程感觉还是很好

好久没看书了，准备空闲时间找本书看看，试试拿过来一直没看的那本《The GodFather》？英文的看起来可能费点劲，坚持一段时间试试

等把哑铃也带到学校，试试晚上锻炼锻炼肌肉



#### 17 周一

周末在家玩了，周日学校的联谊也鸽了，不知道有没有错过什么良缘

上午直接睡过头，睁眼九点半，在宿舍看了看代码

下午晚上看了会ccviewer代码

#### 18 周二

上午下午稍微学了点ccviewer代码，试了试用Qt Designer创建菜单栏

晚上去上了个课

#### 19 周三

上午、下午还是在看ccviewer代码，感觉也没看见多少。。。

这小项目比想象的复杂了些

晚上给涵宝过生日去海底捞聚餐，15人场面，真壮观

晚上9.30吃到12点，第一次体验这种氛围，感觉还不错，不过连着搞肯定是顶不住

#### 20 周四

上午上课

下午在看ccviewer代码，回头看看，感觉这周摸鱼摸得有点厉害，啥也没干，明天又好汇报了。。。

这ccviewer代码也是比我想得复杂，它有些地方写得用到了些高级特性可能，不知道为什么可以这样写，会多花些时间

#### 21 周五

汇报完ppt润了



#### 24 周一

昨天晚上吃完饭11点了，还吃多了，2点才睡，今天好像还有点烧，就在宿舍鸽了，也没学习。。。

#### 25 周二

再宿舍看了看QT基础知识，下午跑了个步运动了运动，晚上上了个课

今天锻炼完看了看感觉有点驼背，需要注意一点了

高低肩也有点，平时也注意些

#### 26 周三

周三去工位学习，但没怎么学进去。

#### 27 周四

上午上课。下午稍微学了会儿

#### 28 周五

早上开了个会，开完会师兄给我分享了下科研经验，也感觉要为开题积累一些理论知识，多看点论文了。

之后就不想学了，放假了



### 五月

#### 02 周二

昨晚跟长辈一起和那个红酒，喝的有点急，有点多了，这酒后劲大，喝了估计4-5杯，大概一瓶多？当时晚上也感觉有些醉了，但没有多难受。

结果回家之后，晚上一点睡觉，中间一直迷迷糊糊也没睡沉，5点多就醒了，然后6-7点钟起床之后，那个酒的后劲上来了可能，开始头晕恶心，饭也吃不进去，难受，吐了一点才好受些，然后慢慢到中午那会儿感觉才好点，但这一天其实都不大得劲。

而且喝红酒感觉真是容易醉，可能还有点过敏，喝了之后喘气没那么顺畅。

以后记得红酒这种的趁着喝，估计也就3杯比较好，再多了之后可能又要难受了。

#### 04 周四

开学第一天，上午上了个课，下午在宿舍看了会儿Qt代码

#### 05 周五

准备了准备汇报ppt，一到汇报的日子就啥也不想干了

汇报完润了

#### 07 周日

晚上去看了电影院看了银河护卫队3，好久没去电影院看电影了，感觉真不错，主要是这电影也好看。

在银河欢乐影城（中国黄岛巨幕），1号巨幕厅，环境很不错，效果也很好，还便宜（32元一个票，吾悦广场卖56元）。离学校也近，走过去15分种左右。下次有好电影还可以去那里看。

#### 08 周一

上午看了看《设计模式》，准备一天最少看10页，一个月看完。

了解了一下smalltalk语言

下午又看了会《设计模式》，完成一天10页的任务。然后去跑了个步。

跑步前买了瓶饮料放在自行车中间那，准备跑完喝的，结果跑完回来，车子倒地上，饮料也不知道去哪了，就很无语。。。

#### 09 周二

看了会设计模式、看了会论文，晚上上课去了

#### 10 周三

看设计模式+论文，晚上爸妈来，一起去吃了个饭。

可能是下午穿衣服少了冻着了，晚上吃完饭回来直接小感冒，有点难受，在宿舍早早休息了

#### 11 周四

上午一上午课。

下午做组会ppt。

晚上开组会。

#### 12 周五

上午跟师兄开会讨论软件开发相关问题，感觉还是得靠自己嗯学，说把之后遇到的问题整理记录一下，然后下次问的时候弄个ppt，这样比较有条理

开完这个会又去看项目组会，纯浪费时间。

开完这个会又让校外师兄帮忙看了看ccviewer编译pcl插件的问题。他那边听说编译之后完全没问题。说我这可能东西装多了冲突了，又说什么vs版本之类的。。。我觉得不该。感觉还是得靠自己。。。但他说要帮我搭个框架，到时候到我的电脑上调通一下，我可能还得按他说的把环境改成他想要的。。。有点烦，完全不想改，我自己用的挺好的。。。

很烦，下午在宿舍打一下午游戏，还是烦。

晚上来工位安了个vs2019来编译，一样的，还是不行。

搞了一晚上，还是没搞出来，我怀疑可能是Win11的问题？不想搞了，我主要是不服气师兄说是VS2022的问题，想给他编出来证明一下，不过我用VS2019试过了，一样的 。不试我也知道，肯定不是这个问题，毕竟都用的msvc2019，能有什么问题。。。



#### 15 周一

今天上午黄师兄把基于ccviewer二次开发的demo发我了，好快的效率，我看了看大致懂了是怎么个二次开发了。那这样的话，编译PCL插件的那个问题好像还真要解决一下。。。

弄了弄还是不行，试了试换cloudcompare源码，用vs2019编译，能像的都想了、都试了，还是不得行。。。

下午在安win10的虚拟机，从头装一下系统看看，就安vs2019+qt5再编译试试。。。

晚上在虚拟机上安qt5.15.2的时候发现qt官网升级了，在线安装包都不提供qt5.15.2的安装了，只有qt6相关的选项。qt5的版本只提供离线安装包了，但坑爹的地方来了。qt5.15.2只提供资源包，你要自己配置环境，然后用cmake来编译，就很sb。。。看着就麻烦，不想搞。再就只能安装qt5.12.12，这个版本提供离线安装包，但这个版本我一看msvc2017。。。就感觉很落后了。。。先装个这个试试吧。。。

#### 16 周二

在昨晚的基础上，上午把虚拟机编译cc需要用的环境都配置了一下，qt5，vs2019，pcl，然后cmak编译，一看还是寄，还是认不出pcd文件，不知道为什么

然后上午剩下时间加下午查了查cc官方的一些答复，看了看可能的原因，但还是没有解决。

然后跑步去了，跑完洗个澡，晚上在宿舍鸽了，顺便看了看《深入理解计算机系统》，稍微复习会议了一下前面的内容，发现都忘了。。。计算人大失格。

#### 17 周三

上午上回体育回去洗了个澡，一看10点半了，又不想去工位了。。。刚去可能就要11点半吃饭去了，干脆在宿舍了。本来想看看《深入理解计算机系统》学习一下，结果玩游戏去了。。。明日方舟抄了个作业时间就过去了。。。

下午回来再查查cc编译出来识别不了pcd的问题，终于看到一个经验贴，说是可能缺了OpenNI2.dll文件，结果我把它复制过去，还真解决了。。。惊了就这个破问题卡我2-3天。。。浪费这么长时间，一方面解决了挺开心，一方面又感觉之前花的时间好亏啊。。。

赶紧去写个笔记去了。

笔记写完直接晚上10点，下班力



#### 18 周四

准备了汇报ppt

汇报

#### 19 周五

准备复习算法分析与设计考试，结果也没复习多少



#### 22 周一

复习算法设计与分析

#### 23 周二

复习算法分析与设计

考试

#### 24 周三

上午体育

下午把mooc考试做了

晚上出去吃了个饭回宿舍了

#### 25 周四

上午做了个ppt

下午汇报了一下

晚上鸽了

#### 26 周五

上午过来学学《设计模式》

跑了个步，下午工位随便学了学？忘了

晚上开了个会



#### 29 周一

上午跑步

下午学了会SARibbonBar的使用

晚上塞尔达。。。（没忍住）

#### 30 周二

继续看了会儿SARibbonBar的资料，试着在VS里配置了一下

有点bug感觉，在Qt creator上也试了试

晚上塞尔达。。。（还是没忍住）

#### 31 周三

上午上完体育开始给贾老师帮忙写了点材料

下午继续帮忙画了个框图

晚上心安理得塞尔达。。。



### 六月

#### 01 周四

VS中见了新项目，把CC封装成库来使用

成功在VS中把ccviewer运行起来，后续在此基础上二次开发

#### 02 周五

开了组会汇报了一下



#### 05 周一

玩

#### 06 周二

最后一节体育

#### 07 周三

啥也没干

#### 08 周四

老师找了谈外派的事，更学不进了

#### 09 周五

没组会，爽玩



#### 12 周一

看了看调用dll中的函数之类的内容，但没啥进展

#### 13 周二

最后晚上集中精神学了一点，看了看代码

话说老师之前问我外派意向的时候我应该表现的够肯定的吧，不会老师没接收到吧。。。怎么到现在一点消息没有。。。

#### 14 周三

学了会ccviewer代码

#### 15 周四

试着自己照着CSDN写了写读取pcd文件的代码

#### 16 周五

准备了组会ppt

#### 17 周六

小舅晚上请客去破店烧烤吃了个饭，感觉地方不错

#### 19 周一

上周组会拖到今天来开

#### 20 周二

继续看了看代码，准备看看拖入ccviewer显示的部分是如何弄的

#### 21 周三

送了送师兄师姐，一块出去吃了个饭

晚上宇突然约我去大连玩，看了看坐船去费劲，飞机有点贵，换成去天津了

#### 22 周四

开始放端午节假，前往天津的路上

#### 23 周五

天津直接热炸，40°高温中出行，脚还磨起泡了，挺了一下午加一晚上

#### 24 周六

做了做天津之眼摩天轮，小逛了一下天津大学，临走吃了顿小老饭庄的饭，被狠狠地宰了

晚上回家，休息休息

#### 25 周日

在家休息，爽玩

#### 26 周一

下午回到学校，稍微学了一点

#### 27 周二

上午起晚了，没干啥

下午试着调一个插件matplotlib-cpp，环境配到5点，幸好最后好使。。

晚上看了一晚上讲小说的，有点头疼，不知道是感冒了还是咋，也学不进去



### 七月

#### 27 周四

今天开始LeetCode每日一题



### 九月

#### 13 周三

LeetCode每日一题从8月15开始放假放下了，到今天还没拾起来。。。

把之前拉下的Qt Creator配置开发环境的笔记补完了

还是得找时间把spring boot 的笔记写了，不过那个在宿舍电脑上写可能得



***

# **懒得每天记了，以后想记就记**

***



## 23-07-07 待做任务

1、GPL开源协议，基于ccviewer开发有无问题？

2、没问题就继续基于ccviewer加功能

3、有问题就从之前qt+VTK读取pcd的那个程序继续来

4、动态显示点云的实验

5、学CloudCompare源码，多窗口界面的设计实现，具体点云处理功能的实现

6、点云拟合的论文阅读



## 23-09-13 待做（完全没做，推到14号了。。。）

1、qt_test中用于显示的vtk-weight独立出来一个ui，并先在mainwindow试验一下

2、实验成功之后，适配SARibbon，直接使用SARibbon试着开发看看

把qt Creator的配置笔记写好了，浪费了好久感觉，主要感觉写的一般

还是得找时间把spring boot 的笔记写了，不过那个在宿舍电脑上写可能得

（上述可记录到日记中）



## 23-09-14

我看今天也悬了，上午调个fgo脚本老出错，一上头搞了搞，花太多时间了，搞到11点，准备该学一下了

老师那边又派过新活来了。。。可能又得推迟一下了。



## 23-09-19

找找叶片几何评价指标及评价方法（论文、CSDN、知乎）



## 23-10-16

软件显示模块，背景色再深点，点云再粗点，让显示效果更明显

去图书馆看看有没有vtk显示模块的书，QVTKOpenGLNativeWidget



## 23-10-23

已经找到实现窗口左下角坐标系的方法

调用PCLVisualizer中addOrientationMarkerWidgetAxes方法

添加ui->qvtkWidget->GetInteractor()即可

详见https://blog.csdn.net/2301_76329543/article/details/130574951

找时间实践一下

## 23-10-24

找到了关于面片细分的相关知识和github程序

需要进一步研究

测试的时候跑loop细分会崩溃



## 23-11-02

网格细分先放了放

先把Property，数据展示部分写了写

找到一个用主成分分析来做圆柱拟合的算法，但效果不太好，要不是参数没设置好还是本身算法有问题，需要进一步研究

目前只用了pcl自带的圆柱模型匹配，能够计算轴线上一点，轴线方向，半径三种数据，但轴线上一点好像是随机的，不是形心，没啥用，要做的话得把主成分分析部分代码完善优化

Property，数据展示部分做出来了，但有很大优化空间

目前，需要点击 拟合 功能按钮来计算，才会展示数据，且计算期间会使程序整体停摆（显示界面无法正常互动）

改进：

- 引入多线程。计算功能肯定要用多线程来做，显示模块需不需要也分个线程来做？多线程了解不多，还需要多探究一下，可能要改代码整体结构
- 在读取文件的时候，后台进行参数的计算，算好了直接展示出来，等后续DB树实现了，可以配合DB树中选中操作来展示
- clean的时候，把这些数据都清空（目前clean没写清空Property的功能）



## 23-11-13

**今日蠢事**：贾老师给展示项目申报ppt的时候，我直接说我有这个ppt，还说了YY给的。后面才想过来这样对YY不太好，毕竟这种ppt好像也是不太想外传，当时老师估计也是不让yy外传，我这一说yy已经给我这个ppt了，就把yy坑了感觉。人家以后怎么看我，估计是觉得这人不得行，以后有些东西都不会跟哥们说了，真蠢。当时就没多动动脑子想想，以后一定得多想想再说。



## 23-11-20

周三的交流

可以提一下后续计划，比如加入多线程操作来。。。



## 23-11-28

今天“优化”程序的时候出现一些问题，同样的变量，只是名字不一样，赋值curr_cloud就可以，赋值给cloud就会报错

最后发现，curr_cloud在一步函数中进行了初始化new操作，而cloud没有进行，导致赋值时相当于赋值给了空指针，导致出错

而在mainWindow.h中声明ptr变量的时候又不能直接new（不知道为什么。。。）

解决方法就是写个initial函数，在这个函数里把声明的ptr指针类型变量都初始化一下，并在最开始运行initial函数即可解决

同样的，声明了一个normal指针，也是没有初始化，导致后续网格化时出错了



## 23-11-30

11月24号晚上的时候把眼睛腿撞断了，第二天楼下眼镜店换了个新的框，结果戴着一直不大得劲，忘了哪天看了眼好像眼镜架旁边一块没装好，自己掰了掰眼睛架，结果掰狠了，金属疲劳了。

在今天晚上，终于是彻底断了。。。血亏138元，都没有坚持一个周。。。

不过感觉这次配的是有点草率，只是大概找了个类似半框，镜框有些部分的角度都没关注，跟原镜框有些地方角度不太一样，导致看东西感觉不对，时间长了会晕。眼镜腿也没太仔细感受、对比，导致这几天戴下来夹得耳朵疼。。。加上导致掰断鼻托的导火索，当时没有关注她给装的镜片有没有把尼龙好好塞进去，结果自己塞进去的时候把鼻托搞坏了。。。下次换镜框要好好看看这些细节，让店员帮忙弄好。。。就当花钱买教训吧。。

## 23-12-01

今天中午去吾悦对面 宝岛眼镜换了新眼镜框，把我爸攒的积分都用了（1200多积分），原价699的框折扣到484，但我感觉他还是卖贵了。。。不过戴着确实舒服多了，因为本来这幅眼镜也是在城阳的宝岛眼镜配的，都有数据，直接找了跟原本眼镜同一品牌的眼镜框，换好之后看东西也没觉得晕了，也不夹耳朵了

就是换镜片的过程有点。。。原来都是手工换的，看他换的过程感觉好暴力。。。生怕把我镜片、镜框搞坏了。。。今天装完检查了一下尼龙线有没有被挤出来，左边框左右两边都挤出来了，让他帮着塞进去，虽然最终是塞进去了。。。但是他弄得也挺费劲的，过程还贼哈人，还跟我说这是正常的，硬搞别把框整坏了不值当的（我寻思你弄坏了不负责吗。。。）。而且我一直以为他们有工具会好弄呢，结果看着也不得行啊，可能真不如我回来自己搞搞。。。

下次在装的时候提醒他注意一下这些细节可能会好，装的时候就把这些边角尼龙都对准了再装，应该比到时候再塞进去容易多了。

最终有惊无险两边都弄好了，不过左边鼻托当时塞尼龙绳的时候被他搞得抬高了，又让他给我用工具调回来了，不知道这一下会不会影响这个鼻托的寿命，毕竟学校那个框就是鼻托掰狠了直接断了。。。这个这么贵的别再搞坏了。。。不过应该也问题不大，克服一下心理因素

话说他调没调彻底，我看左右鼻托还是有点高低不平，这次我也不敢手掰了，网上买了个工具，到时先用学校配的那个框试验一下，然后自己调整一下，右边的鼻托应该是初始状态，照着把左边的稍微调整一下。。。

***

今晚仔细看了看他给我塞尼龙线的地方，镜片、镜框都被划了一点，以后这种事问一下他好弄吗，不行还是算了，可能真不如自己弄仔细。我看他那也没有专业弄这个的工具，一开始没装好，估计也就没辙了，他弄肯定不如咱自己弄耐心细心，手艺这么糙，真划伤了镜片心疼死。自己弄的点小瑕疵就罢了，他给弄出来的小瑕疵心里更难受



## 23-12-04

最近是有点点背，前两天眼镜框撞断了，换了两次，适应了几天终于这事差不多算过去了，今天又被马蜂蛰了一下。。。

它不知道怎么钻在我秋衣里，我一穿秋衣，突然手臂跟触电一样疼，我赶紧脱下来，过程一开始还以为听到摩擦静电的声音，以为真是被静电电了，但静电又不会这么持久，反应过来像是蜂子的嗡嗡声，脱下衣服来果然有个马蜂飞到窗帘上去了。。。

去校医院看了看，也没什么大事，倒是学到了马蜂的毒是碱性的，要抹点酸性的东西；蜜蜂的毒是酸性的，要摸碱性的，比如肥皂水。

去超市买了瓶白米醋，摸了摸，到中午基本不肿了，就是被蛰的地方还有些红，问题不大。应该是蛰的不是很厉害，加上蛰在手臂上，我一直挤着被蛰的地方，毒素应该没扩散太多。

## 23-12-11

今天取快递，圆通快递那个女的真是<span style="background:#000000;color:black" >一坨臭狗屎</span>。买的四本一套的书，有个书盒，去那一看，这包装。。。就外面一个袋子，拆开验货，果不其然，撞角、挤压。直接去找圆通柜台拒收，那女的不知道为了冲业绩还是怎么地，让我别拒收，走运费险退货，我当时想着天猫超市买的，退款应该秒通过，结果<span style="background:#000000;color:black" >tnd</span>他不支持七天无理由，还要在那审核，我还得等着它审核好了才能走退货流程，那不还得跑一趟，纯纯浪费我时间，直接拒收哪有这么多<span style="background:#000000;color:black" >b</span>事，我也是<span style="background:#000000;color:black" >sb听她娘的</span>，以后不用管<span style="background:#000000;color:black" >tm</span>的，我就要拒收<span style="background:#000000;color:black" >你娘的</span>。<span style="background:#000000;color:black" >真尼玛的臭傻逼。</span>



## 23-12-17

最近飞来上海进行交流学习，本来以为是过来接受一点软件开发方面的培训就回了，结果好像不是那么回事，要想学到东西，需要进行一个长期的实习，在实习中学习，又问了问老师关于实习时间的事，老师说都行，你随便实习，对你提升有帮助就行。老师对我的关心我很感激，不过我也担心最后这个实习到底能否对我产生很大提升，我怕只是还是给一个项目，自己进行摸索，那感觉就没啥必要了呀，学校那里的项目还是要自学着做，还关系到中期、毕业之类的。。。好纠结，我也不知道敢不敢到时候说帮助不大我直接不实习了，因为我也怕这就是我单纯懒、不想干产生的抵触心理。

明天跟公司老总再交流来看看，这次把得到的信息，充分交流一下，把话说明白。本来老师可能就是想让我过来接受一个10天半个月的软件开发方面的培训，提升一下软件开发的能力。后续想继续学的话，再去青岛分公司继续。不过话也说回来，这毕竟也不是我家开的公司，想来就来、想走就走啊，可能还是做好要进行一段时间实习的准备吧。。。

而且中途退出，虽然说可以，但可能也有点伤老师的面子，不太推荐这样做，所以明天尽量把所有问题都问清楚：1、实习时间，说是都行，但考虑到研究生的一些事，半年最多了，研二下半年应该还行，这半年反正可能要累些，一方面搞实习，一方面搞搞学校的项目（不过不知道到时候下班还能有精力搞吗。。。另外这只是搞项目、科研方面不知道能弄吗。。。而且实习话说也不知道好搞吗，别下班了还要加班之类的吧，话说实习项目到实习结束一定要能做出来吗？是每周有个进度安排、还是就反正你后得把这个目标做到，不然不行这样。。。）2、实习内容，毕竟目标还是主要提升软件开发方面的能力，考虑到跟毕业内容相关，最好能跟点云处理相关。最好还要知道实习期间有人带吗，不会还是给个目标自己弄吧。。。那感觉就是纯干活，没啥必要了吧。。。我自己在学校里加把劲督促督促自己学学感觉还轻快些。3、关于软件开发方面的提升：我现在自己开发软件感觉就是野路子，咱们企业这边开发软件，不得有些设计规范、类的设计，总之就是想看看企业中开发一款软件都经历那些流程、过程，所以本来寻思整个10天半个月小培训就行。

最后怎么就聊着就变成实习了呢。。。不过确实，听老板说的，人工智能专业，之前我对它的理解就局限在神经网络、深度学习方面了，我对软件控制硬件这些东西真是不怎么接触，如果通过实习，能对这些东西有一个掌握，那感觉也行，毕竟就让我在学校自己学个半年，感觉也没啥大提升。。。

***

**近两周汇报内容：** **1、构思设计用来存带点云数据的自己的数据结构MyObject**，具体思路见“类图.md”。设计这个主要是更好地分类存储数据（点云、基于其产生的法向量、网格），也方便文件树的展示、参数的展示。说到这，要不要把**点云的一些参数**也加到这个类里？**2、CSDN找到一个**做了DB树模块、做了DB树中item选中、做了选中后获取数据的程序，发现它里面读点云用vector，能存多个点云数据，这个思路也学一下。**3、**本来应该是能把上面<span style="color:red">DBTree优化差不多</span>，然后再能稍微加点<span style="color:red">多线程试一下</span>的，结果周三晚上老师跟我提了去上海的事，我跟上海联系了一下，想着快去快回，就周四飞到上海，花了一天。周五给我看了看公司产品，给我看麻了，花了一天。周六出去逛了逛，花了一天。周日，今天随便看了点东西又结束了。**4、做了点数据**，把原来圆柱点云数据两头底面数据给去掉了，本来还要<span style="color:red">做点加噪声的数据，给程序加个去噪功能</span>试一试来着，也没做。。。

***

好久没坐飞机业务都不熟悉了，计划是11.30收拾好行李出发，坐2小时地铁去机场，1.30到，2.45的飞机提前一小时到应该还行，不过出去走在路上发现忘带身份证了，回去取了之后感觉有点赶，就打了个车过去了（打车130+），12.30到，提前了两小时，事后感觉没有吃饭之类的需求，去了就是托运、值机的话，提前1小时就足够了，绰绰有余。飞过来说是要到16.25，不过16.就着陆了，但对地方不太熟，找约的司机的位置找了半天，最后5.才找到司机，去到公司5.35了，效率不高。

回去的时候还是做高铁算了，车上还能联网办公？看看吧，看我有那个精力吗还。。。

***

**当前桌面状态：** 

- Firefox：

  - PCL+QT开发https://blog.csdn.net/weixin_43236944/article/details/123536625

  - Poe：隐藏点云、代码解释

  - 获取QTreeViewer选中行内容https://blog.csdn.net/naibozhuan3744/article/details/92573309#:~:text=1.1%E6%A0%B8%E5%BF%83%E5%87%BD%E6%95%B0%20%E8%A6%81%E8%8E%B7%E5%8F%96QTreeView%E9%80%89%E4%B8%AD%E8%A1%8C%E5%86%85%E5%AE%B9%EF%BC%8C%E5%8F%AA%E9%9C%80%E8%A6%81%E4%B8%A4%E8%A1%8C%E4%BB%A3%E7%A0%81%E6%90%9E%E5%AE%9A%EF%BC%8C%E4%B8%80%E4%B8%AA%E6%98%AF%E7%BB%91%E5%AE%9A%E7%82%B9%E5%87%BB%E9%80%89%E4%B8%AD%E8%A1%8C%E4%BF%A1%E5%8F%B7%E5%92%8C%E6%A7%BD%E5%87%BD%E6%95%B0connect%20%28...%29%EF%BC%8C%E5%8F%A6%E4%B8%80%E4%B8%AA%E6%98%AF%E5%9C%A8%E6%A7%BD%E5%87%BD%E6%95%B0%E4%B8%AD%E6%B7%BB%E5%8A%A0%E5%87%BD%E6%95%B0%20QTreeView%3A%3Amodel-%3EitemData%20%28%29.values%20%28QModelIndex%29.toString,%EF%BC%8C%E5%A6%82%E4%B8%8B%E6%89%80%E7%A4%BA%EF%BC%9A%20treeView%20%3D%20new%20QTreeView%20%28%29%3B

  - 类图https://mermaid.nodejs.cn/intro/

- VS：CloudMeasurement，把MyObject类创建出来，写了点get、set方法，在想加点函数，直接计算出法向量、网格？
- VS Code：CloudCompare，看看ccDBRoot咋写的，怎么个逻辑，看不太懂
- Qt Creator：CSDN买的那个程序，在看它的QTreeViewer选中行相关操作、读取点云到Vector，在想自己的读取，是弄个Vector\<MyObject>还是咋弄的。。。
- Typora：临时文档（有记读取文件相关代码，只读pcd的和CSDN那个能读ply、pcd的），类图
- CloudCompare：随便打开做参考的，还看了下用去掉地面的圆柱点云生成网格化的效果，发现跟原来一样，没影响。







## 23-12-21

前几天的心得可以补一个

**回去之后的几个要学的点：**

- python控制相机、控制机器人、控制采集点云数据，深度学习处理点云数据——马钰
- 电路板设计、绘制、检测（查哪个引脚有问题之类的），单片机编程、与硬件通讯、上位机软件——张欢
- 相机跟计算机的通讯，图像处理，相机的相关知识——师良师兄
- SolidWorks的使用、设计——向阳
- 深度学习原理等——哲豪
- ROS、RobDK，计算机对机器人的控制——陈晨师兄
- 控制机器人扫描得到测量点——林波师兄

**可能需要的硬件：**配一台显卡好一点的电脑，跑深度学习（想想是弄笔记本还是台式机，台式机的话配置好远程控制，放在工位？宿舍？）也问问马钰他研究了这么久，深度学习处理点云数据处理地过来吗？咱自己配的显卡够用吗？



***

**最近的心得：**实习还是第一份工作，感觉还是得去华为这样的顶尖大厂里去，去看看人家企业的规范，去看看一流公司的开发流程，增长眼界。

去这种小厂，总是不服气，觉得不规范、不专业，难道真是咱太浮躁了吗，咱真的只配在这种地方 工作吗，我不甘心、不服气

一个是增长见识、一个是证明自己、提升自我认同感。

***

**回去之后的安排：**

- 一方面，跟进自己的项目，不过感觉开发重心已经不能在软件设计上，重心要往算法上偏移。先集中看看**点云去噪算法**能不能做出点东西来，最后实在不行靠软著毕业

- 另一方面，根据上面列的点，找对应的人，补充学习对应的知识，毕竟在这个组里，组里的研究核心还是要多接触，不用做多深，自己能上手实践一下的程度应该就行。

- 最重要的一点，去牛客网看面经、刷题，买本《剑指offer》实体书吃透，把C++的一些特性熟练。准备**华为实习的应聘**。一是去真正的学习一些东西，二是（内心迫切地想）证明一下自己、增强自我认同感。**目标暂定**——24年**3月份**的暑期实习

  - **面试**——https://www.zhihu.com/question/36560542

    关于笔试面试的准备我前面没有说，在这里集中说一下吧，国内有一个叫做**[牛客网]**的网站，里面有很多面试/笔试经验贴，包括**准备过程、参考书籍**啥的都介绍得很全面，非常具有参考价值。

    我在面试之前只刷了一本书: **[剑指offer]（C++版）**，因为我投的都是C++相关的岗位，所以用了这本书。面试的时候，一是语言本身，二是算法，这两个东西一定要熟练。语言主要是一些特性，以C++为例，类、友元、运算符重载、封装性、传参by reference或者by value的区别（C++别跟我提指针好吗？）、拷贝构造、拷贝赋值等这些概念非常重要。如果是C++岗位的话，STL也要有相应的了解。一定要看C++ Primer啊，国内的教材（包括网课）没有一个像样的，如果有的话，请一定要告诉我T^T  

    算法就不多说了，一句话： 看一遍数据结构，然后赶紧刷起来。（牛客网有许多经验贴）



## 23-12-22

**几种需要掌握的算法：**

- 树：文件树应该用这种数据结构来存比较好，去好好参考一下CLoudCompare源码
- 线性回归/逻辑回归：深度学习的基础



## 23-12-23

**想到一个想尝试的点：**结合神经网络、AI

现在AI大火，做什么都在想跟AI结合，点云处理的一些算法尝试用AI、深度学习的方法来做，之后配置用软件来调用这些智能方法



## 23-12-24

- **备选方案：**直接在CLoudCompare的基础上进行插件开发，实现我们自己优化的点云处理、几何评价算法
- **需确认：**GPL协议，开发的插件的源码需不需要开源？
- **可能的问题：**插件开发，实现的点云处理功能，使用的数据结构是要依托于CLoudCompare自定义的数据结构吗？就是还是需要搞懂CC中点云数据读进来之后存在哪里，如何调用这些数据吗？



## 23-12-25

这两天看牛客网上一些帖子，给我看焦虑了，看完就感觉完全找不到工作了，互联网开发要学的东西爆炸的多，根本没有精力都学一遍到能面试的程度感觉。

简历上有好的项目经历、实习经历的，感觉机会就很大。然后就开始反思把之前力信测量的实习给推出去了到底是不是好事，我会不会因为错误的判断失去了一个很好的机会？

但通过我那几天了解到的，在那里要真学到些东西，可能得1-2个月起步，而且环境是很大问题，如果是能收获满满，环境其实无所谓，习惯一下就好，关键是我感觉也就是给布置一些任务，然后自己摸索着来学习，跟在学校比的区别可能就是那里任务明确些，更有方向性？

不管怎么样，既然决定都已经做了，就不要再后悔，谁也不知道未来的事如何，在那里实习一段时间，可能很有收获，可能收获不大。但既然已经做出了判断，回学校学习收获的会更多，就要努力不辜负自己的这份判断，不要让自己后悔。回来学校了，一定要把时间充分利用起来，抓紧时间学习，提升自己的能力。

找工作这块，也别太在意牛客网上的这些帖子，一方面他们大多数找的是java相关的工作，另一方面他们主要盯着字节、腾讯这种现在顶尖的互联网公司。这种现在极热门的公司就是竞争很激烈，java工程师又多（据说），是会难找一些。

相对来说，我的第一志愿一直是华为，以及偏向C++软件开发的方向，相比于他们，竞争应该会小一些，当然也不好说，但焦虑也没有用，还是按照自己的节奏，按照当初定下的计划来实施吧，只有真正沉下心来做了，才能知道到底如何。

**备战3月份华为暑期实习**

**计划：**

- 1、工作时间：8:30——17:30，国家重点研发项目推进
  - 软件结构的不断设计、优化
  - 核心算法的实现
- 2、其余时间：自我提升
  - 刷算法题、学习数据结构（在平时的开发中也尝试看看能不能用上，不然刷这些的意义在哪？只是为了入职的机试吗？）
  - 扩展、深入研究C++、操作系统等知识点（最终也要落实到日常的开发中）
  - 学习一下深度学习相关（可以放到工作时间，尝试用深度学习的方法实现点云处理核心算法）

然后也不要太焦虑，尽力而为，不要让自己后悔。实在不行考个公务员？读个博去高校当老师？接受失败的事实，找个工作踏实干几年。

