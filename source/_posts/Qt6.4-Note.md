---
title: Qt6学习笔记
date: 2023-04-17 21:14:46
tags: Qt
category: 笔记
---







## QAction

### toggled()

toggle 类似开关。 具有2个状态，打开/关闭。  使用这个信号，是在这2个状态之间切换。checkable按纽或是图标的槽函数应该用toggled()事件来激活

### triggered()

trigger是一次性的。 点击后，无法改变状态。 要么是打开，要么是关闭。一般的按纽（uncheckable）的激活方式即是triggered()。更有触发的意思。这个单词还有另一个意思就是板机

