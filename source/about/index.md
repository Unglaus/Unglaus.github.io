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

## 2023年3月

### 06 周一

今天本来是想试试Qt+VTK+PCL显示点云数据的，看了看如何QWeight提升为QVTKOpenGLNativeWidget然后使用，一直没实践，明天试试在Qt Designer里提升再编译，看看源代码怎么生成的，然后在学学怎么用来显示PCL点云

主要时间在试各种C++库在VS中配环境的办法，基本试出来了，明天整理整理些blog

就因为想写blog，又弄了弄hexo的配置，显示那个前端加密插件没发挥作用，搞了一会儿没搞出来，然后突然发现可以typora存图片到文章同名文件夹再发布上去，方便管理。不过在本地的图片相对路径是test/aaa.imag，而发布到hexo之后，它自动把文件夹合并了，md和img放在一起，所以发布到网上的图片的路径需要时aaa.img，相较于本地md文件中的路径少了前面的文件夹相对路径。为了让它上传时自动把路径改变，找了半天插件，最后找到hexo-asset-img这个插件可以实现我的要求，已加入收藏夹“hexo插件”中。

这样相比于传到图床上更安全，一方面本地图片都有各自的同文章名的文件夹，方便管理，上传到hexo的部分也都是md和img在一起，也很方便查看。

最关键的是我用github做图床时，本地加载不出来，网络上不挂梯子有时也看不了，很蛋疼，这样最好，最起码本地一定能看，不需要另外配一些东西。

### 07 周二

今天上午稍微调了一下QVTKOpenGLNativeWidget在Qt中的配置，在Qt Designer中拖动QWeight并将其提升为QVTKOpenGLNativeWidget，然后编译，看源代码的生成。其中有一点要注意，需要将VS属性中Qt setting的model部分勾选QVTKOpenGL，因为QVTKOpenGLNativeWidget是继承自QVTKOpenGL的，不然会有错误，具体见blog。然后被向阳叫去帮他看程序，帮他配了一下Qt新窗口同Qt Designer绑定。再然后被拉去打扫实验室卫生，隔三差五打扫卫生。。。随便弄弄又到饭点了，一上午草草结束。

下午摸鱼摸到4点，摸到方舟怪猎联动开服，抽了抽卡，打了会儿关卡，感觉也没干什么就到5点了，然后又被向阳叫去帮他看程序，关键看了半天也没解决，晚上还有课，昨天说要写的blog还是没写，又要拖到第二天了，就感觉一天了自己的事儿一点没弄，搞得很烦躁。

晚上就是上课，算法分析与设计，不知所云，纯坐牢。下课九点半，回宿舍洗洗澡，玩玩密特罗德：生存恐惧，结果又迷了一晚上路，最后发现是因为新地图有条路被隐藏砖挡住了，这个隐藏砖需要变成球放的紫色炸弹才能打开，一开始没找到导致我把所有图几乎又跑了一遍，等找到这条路都11点半了。（这条是第二天回工位写的，不然一般记录是在工位写完回宿舍玩去了，晚上的游戏记录一般不会写）

### 08 周三 

上午又帮向阳看了看程序，最后还是搞不定，这东西我需要自己花一段时间学，没学过直接给我叫过去看半天我也弄不来啊，弄到大概10点放弃了。然后写了会OCC+VS配置的blog，稍微去4楼干了点活，结束

下午过来坐着想把那些教程blog都补上，林波师兄过来问PCL初始显示点云的时候默认追踪点云显示，我也不会啊，稍微看了看，没找到相关代码。然后贾老师又让去统计小组要买的白大褂的尺码，去找业茹师姐要了购物链接，然后看了看，做个excel，也没弄什么半天过去了，再一看时间已经4点半了，这周还啥也没干呢。。。

晚上一直在写OCC+VS安装及配置，没想到写了那么久，到最后也没写完，还差一点

### 09 周四

把昨晚差的哪一点小教程写完，结果没想到写完11点了，一上午基本过去了，这周组会讲啥啊。。。

下午，干了什么来着。。。

晚上在看CloudCompare Wiki学习一下软件的使用，然后又自己试了试，大部分时间摸鱼玩方舟去了。。。

然后想着把Qt配合VTK显示点云给弄出来，结果遇到一堆问题，弄半天弄到11点了，服了，明天早上稍微试一下，还不行就随便做个ppt，汇报完再弄吧

### 10 周五

弄了一上午，没有什么结果，具体去看blog，不过基本确定了，应该就是两个vtk版本都放一块可能有点冲突，还是要吧自己编译的vtk9.2覆盖掉pcl自带的vtk9.1，然后重新编译一下pcl，这样应该就没问题了。不过因为要开会来不及了，所以先把ppt做了，这个重新编译pcl之后再试吧

2点跟杜二宝师兄开了个会，确认了一下当前开发点云处理软件的配置，杜师兄说就在windows下弄就行。另外，说我那个圆柱点云拟合出来的数据肯定不行，再查查论坛啥的看看别人怎么弄的。

开完组会之后就啥也不想干了，到点收拾收拾走人了，晚上跟欢儿打了打乒乓球，欢儿兵乓球有一手的。

### 11 周六

跟毅他们约着出来玩。

<span style="background:#000000;color:black" >本来约的下午一点半，结果某强愣是睡过头，最后下午五点才来。</span>

打麻将打到9点，回学校10点半，玩了玩睡了

### 12 周日

密特罗德：生存恐惧通关，又花了2小时左右全收集了一下，然后打了打boss rush模式，好玩的这游戏。不过就买个二手卡带玩玩，玩完再出了就好，毕竟300+的话，感觉还是。。。



### 13 周一

尝试一下用自己编译的vtk9.2配合pcl自带的其他3rdpart重新编译pcl1.12.1

编译PCL的时候照着别人的教程设置了pcl_find_boost.cmake，手动添加了boost 的include和lib位置，结果还是cmake的时候还是找不到boost的位置。最后发现是因为文件夹路径中含有空格“pcl 1.12.1”导致的问题，将路径中含有空格的文件夹名称更改，去掉空格之后，cmake的时候就能顺利找到boost 了

我又试了一下，果然就是因为路径里文件夹名字有空格，它就会找不到路径，把空格删掉就能正常找到路径

之后就是正常编译PCL，然后稍微改了下环境配置，再跑一下代码，果然没有问题，搞定，写写blog收个尾。

### 14 周二

昨天关于PCL配置的blog没写完，争取上午写完

惊了，写了一上午加一下午还没写完，效率太低了。。。摸鱼摸得有点过了。。。

晚上又要去上听不懂的课，上完回宿舍玩去了。。。

主要写教程的时候因为我安装过了，有些图不太好搞，我又不想把配好的东西删了重新配，配图片画的时间多了点。。。

考虑要不要先文字描述，然后把图片位置流出来，等在新电脑配的时候再截图。也不是不行。

## 15 周三

上午。。。上午好像没干嘛，有印象的就是把PCL配置那个教程又写了写，但还是没写完。

下午试了试OCC+Qt读取Step文件，一开始总是报错，最后发现，其实是因为文件读取路径用了反斜杠，导致文件没有读出来（**突然认识到，读文件时加一句if判断，如果文件为空，弹出提示这种语句的重要性了**），文件路径的反斜杠改成斜杠就行了。以后记得在读完文件之后，后续要执行的语句外加一个if判断，判断该文件不为空再执行，若为空返回个提示。这样也不至于卡半天了。。。

然后突然对OCC的Qt例程中使用myObject3d.Append()这种方式显示模型的方式感兴趣了，也学了一点点Qt，这次再去试试能不能看懂。

结果晚上睡着了，醒了8点半，写了写PyCharm缓存移到别的位置，就结束了

## 16 周四 

看了看Qt程序的执行过程，把它的项目文件结构搞明白了，然后写了个blog总结了一下

晚上学了学vue，他官网给了个互动教程，感觉不错，把常用的组件以及简写都说了一下，就比如它常用的Attribute绑定，`v-bind`指令，拿`div`举例`<div v-bind:id="dynamicID"></div>`，其中的`v-bind`一简写，就变成了`<div :id="dynamicID"></div>`，就剩个冒号了，这一般还真不知道是个什么意思，也没法查起。还有事件监听，`v-on`指令，拿`button`举例`<button v-on:click="increment">{{ count }}</button>`，可以简写为`<button @click="increment">{{ count }}</button>`，这种@的写法我感觉还真见过不少，当时没学不知道是什么意思，原来是事件监听`v-on`的缩写

然后写了写周五上午和下午两个组会的ppt干到11点，一天又结束力。

明天开一天会估计也不想干什么，回首这周感觉啥也没干啊。。。

明天干脆把blog补一补收工算了。。。这能毕业吗。。。

## 17 周五

上午开完，下午开，开完啥也不想干

<span style="background:#000000;color:black" >晚上还被PUA，叫我去玩，我不想去，结果都不去了？什么鬼啊</span>

<span style="background:#000000;color:black" >还有班里组织个活动，也不先统计个人数，直接搞了个2500的别墅，去的人少直接资金爆炸，还来催人，催过来催过去，差不多得了</span>



## 18 周六

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



## 20 周一

课题组给配的电脑来了，开始在新电脑上安装需要用的软件。

不过在安新软件之前我发现当时win11激活时直接用的微软账号，所以C盘用户文件夹的名字直接是我的邮箱前5位，很难看，然后我去查怎么安全的改这个名去了，就这估计搞了一上午，下午才开始安各种软件。

安到hexo的时候在想，怎么让两台电脑的hexo博客同步啊，然后去查，然后照着配置，结果配完之后在测试的时候发现git pull的时候本地文件没更新。然后一直在尝试，试到晚上都没试出来，卡住了。

## 21 周二

安了安其他软件，然后又去搞昨天卡住的hexo多设备同步问题去了，之前只是照着配，这天去看了看具体的原理之类的东西。

下午两点去搬东西，弄完回到工位三点半了好像。

然后下午又想试一试昨天git pull那个问题的时候，发现在原电脑git push的时候出错了。然后也没弄了，晚上上课去了。

## 22 周三

上午查了查之前git push出的错，然后又测试了一下git pull，发现成了，之后两台电脑都测试了一下。可以互相git push 和git pull了，也就说终于配置好了，之后就不怕在工位写的blog和宿舍写的blog冲突了。

可以开始愉快的更新blog了，准备把更几个blog，这次hexo多设备同步的步骤更一个，更改win11用户文件夹名字更一个，再稍微弄个小的git笔记？

然后一下午把之前旧电脑上的项目git到GitHub上。晚上试试pull到新电脑上

在pull的时候基本上很顺利，通过这种方式比u盘直接拷贝快不少，当然前期准备也复杂一点。

但是还是遇到了问题，pull下来的项目中，与qt有关的项目都找不到头文件位置，可能是因为qt安装的位置不太一样，加上qt的小版本也不太一样，他现在只有在线安装包，当时安的时候是6.4.0，过了几个月？就变成6.4.3，之后都没有6.4.0的安装包了，这我咋办。。。

找了找vs里qt可能的环境配置的位置，找不到，搞不懂，想了想干脆在新电脑上把Qt有关的项目重新建一遍，然后把pull下来的代码复制上去。之后如果想搞同步的话，把旧电脑原来的qt6卸载，安装到跟新电脑一样的位置，反正得保证至少有一边是能用的。其实如果两个电脑qt安装的位置一样的话，可以试试把旧电脑上的qt用它自带的安装包更新一下试试。

然后因为是vs+qt创建的项目，所以可能还要注意一下qt vs tools的版本？

<span style="background:#000000;color:black" >话说今天电梯的见到一个长得对胃口的妹子，但是男朋友就在旁边。突然就有点emo，像这类女生都有对象了吗，到现在了都多久没谈过对象了，是不越往后找到没谈过的几率也少了，或者说剩下的没谈过的会不会都是我看不上的那种？或者说以后找的对象她有好几个前任，接受的了吗？就想想就感觉是不是要抓点紧了？但想了想又不知道从何下手，一是看到有感觉的妹子感觉几率不大，主要是自己参加的活动太少，但你说看见了吧，也是像今天这种路上遇到，今天这个旁边有对象，但就是没对象我也不太可能上去跟人家搭话。。。这种感觉好像就是上次班里轰趴给加重了，就看着那些女生我就感觉。。。周围只有这种的了吗。。。可能加深了这种焦虑，感觉完全没有我的菜。。。好姑娘可能都无了，以后就算有可能也都有过前任经验，而不是完完全全属于我的那种的感觉。。。精神洁癖？寄。。。以后难道只能靠相亲找个没有感情的，然后两个人搭伙过日子这样了吗。。。好惨一男的。。。</span>



## 23 周四

<span style="background:#000000;color:black">晚起的人有漂亮妹子看。</span>

昨天晚上把Qt相关的工程在新电脑重建了一下，也没干什么好像，但就是待到挺晚，回宿舍都12点了，睡觉的时候快一点了，不能再这样了，不然早起真顶不住，而且老睡这么晚身体不行，脸上都疯狂爆痘了。

今天在床上墨迹到8点半才下，出发去工位都九点了。<span style="background:#000000;color:black">不过今天在电梯间又看到了漂亮妹子，对胃口的那种，不知道有无对象，就假定没有，稍微缓解了一下昨天晚上的焦虑，看见漂亮妹子就是开心。</span>

<span style="background:#000000;color:black">突然想到，之前那种焦虑，也有很大一部分原因可能是B站刷到的那类相亲奇葩视频搞得，看这些牛马看多了，就感觉没正常人了，真服了，就看那些傻卵东西看的，导致我觉得自己对妹子心态都不正常了。</span>

重要结论：没事少看B站。<span style="background:#000000;color:black">现在B站也就是新型垃圾场，什么负面垃圾新闻到处是，看多了人能好就怪了。尤其那些相亲相关视频，净把些狗屎拿出来讲，来恶心人。</span>


