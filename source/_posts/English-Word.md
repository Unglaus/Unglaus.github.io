---
title: 大家一起学英语
date: 2023-03-07 15:34:56
tags: English Word
category: 英文学习
---

## 引言

在学习OCC、PCL等C++库，或是其他一些技术时，通常需要阅读官方提供的技术手册，而这些手册大多是英文编写，虽然可以直接使用翻译软件进行翻译，但毕竟翻译软件有时翻译的也是词不达意，加之它可能把人家定义的类名之类的东西也翻译成中文，还不如直接看英文。综上，长远来看，提升自己的英文水平总没错，本文用来收集阅读英文手册或教程时遇到的各种不认识的单词，也不指望能将这些单词全部融汇贯通，但希望下次见到时最起码能认得它是个什么意思。

### OCC

- geometry：几何学
- parametric：参数
- dimension：纬度
- infinity：无限大
- second order：二阶
- criteria：标准
- scaled ellipse：缩放的椭圆
- cylinder：圆筒
- conjugate：共轭的
- projection：投影
- intersection：交叉点
- topology：拓扑学



### PCL

- complicate：复杂化
- trim：修剪
- outliers：离群值、异常值
- deviation：偏差



### CloudCompare Wiki

- mesh：网格
- portable：便携式（可移植）
- trade-off：权衡利弊
- entity：实体
- property：属性（财产）
- scalar：标量
- scale：规模、刻度
- align：对齐
- alignment：对齐
- registration：配准（注册）
- fine registration：精确配准
- primitive：原始的、基础的
- primitive factory：基体工厂（创建基础模型）
- cloud/primitive Dist：点云/基体距离
- merge：合并
- subsample：子样本
- Octree：八叉树
- histogram：直方图
- projection：预测
- SF（scalar field）：标量字段
- rasterize：栅格化
- volume：体积
- statistic：统计数据
- ALS：机载激光雷达扫描
- TLS：地面激光雷达扫描



### Octree Wikipedia

https://en.wikipedia.org/wiki/Octree

- Octree：八叉树，用来将3维空间递归地细分为8个卦限，它相当于三维空间的四叉树
- Quadtree：四叉树，用来将2维空间递归的分为4个象限。
- octant：卦限，类似于于二维空间的象限，一维空间的ray
- quadrant：象限
- ray：射线（？）
- recursively：递归的
- subdivide：细分
- analog：模拟、类似
- dimension：纬度

#### Implementation for point decomposition

The example recursive algorithm outline below ([MATLAB](https://en.wikipedia.org/wiki/MATLAB) syntax) decomposes an array of 3-dimensional points into octree style  bins. The implementation begins with a single bin surrounding all given  points, which then recursively subdivides into its 8 octree regions.  Recursion is stopped when a given exit condition is met. Examples of  such exit conditions (shown in code below) are:

- When a bin contains fewer than a given number of points
- When a bin reaches a minimum size or volume based on the length of its edges
- When recursion has reached a maximum number of subdivisions

```matlab
function [binDepths, binParents ,binCorners, pointBins] = OcTree(points)

binDepths = [0]     % Initialize an array of bin depths with this single base-level bin
binParents = [0]    % This base level bin is not a child of other bins
binCorners = [min(points) max(points)] % It surrounds all points in XYZ space
pointBins(:) = 1    % Initially, all points are assigned to this first bin
divide(1)           % Begin dividing this first bin

function divide(binNo)

% If this bin meets any exit conditions, do not divide it any further.
binPointCount = nnz(pointBins == binNo)
binEdgeLengths = binCorners(binNo, 1:3) - binCorners(binNo, 4:6)
binDepth = binDepths(binNo)
exitConditionsMet = binPointCount<value || min(binEdgeLengths) < value || binDepth > value
if exitConditionsMet
    return; % Exit recursive function
end

% Otherwise, split this bin into 8 new sub-bins with a new division point
newDiv = (binCorners(binNo, 1:3) + binCorners(binNo, 4:6)) / 2
for i = 1:8
    newBinNo = length(binDepths) + 1
    binDepths(newBinNo) = binDepths(binNo) + 1
    binParents(newBinNo) = binNo
    binCorners(newBinNo) = [one of the 8 pairs of the newDiv with minCorner or maxCorner]
    oldBinMask = pointBins == binNo
    % Calculate which points in pointBins == binNo now belong in newBinNo
    pointBins(newBinMask) = newBinNo
    % Recursively divide this newly created bin
    divide(newBinNo)
end
```









不定期更新中。。。

