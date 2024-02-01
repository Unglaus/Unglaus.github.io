---
title: CloudCompare源码学习笔记
date: 2023-04-19 10:51:00
tags: 
- Qt
- cloudcompare
category: 笔记
---



# ccViewer

## 代码解析

```c++
ccViewer::ccViewer(QWidget *parent, Qt::WindowFlags flags)
	: QMainWindow(parent, flags)
	, m_glWindow(nullptr)
	, m_selectedObject(nullptr)
	, m_3dMouseInput(nullptr)
```

这段代码是一个类 `ccViewer` 的构造函数的实现，该类是继承自 `QMainWindow` 类的。

构造函数的参数 `parent` 是一个指向父窗口的指针，参数 `flags` 是窗口的标志。

下面是成员变量的初始化：

- `m_glWindow` 是一个指向 `QOpenGLWidget` 对象的指针，初始化为 `nullptr`。
- `m_selectedObject` 是一个指向选中的对象的指针，初始化为 `nullptr`。
- `m_3dMouseInput` 是一个指向 `Q3DMouseInput` 对象的指针，初始化为 `nullptr`。

在这个构造函数中，这些成员变量都被初始化为默认值。这些成员变量可以在类的其他成员函数中使用，以实现类的功能。



---

```C++
connect(m_glWindow, &ccGLWindow::filesDropped, this, qOverload<QStringList>(&ccViewer::addToDB), Qt::QueuedConnection);
```

这是一个Qt中的信号与槽连接语句，用于连接一个发送信号的对象（`m_glWindow`）和一个接收信号的对象（`this`，即当前对象）。

具体来说，这条连接语句的含义是：当`m_glWindow`对象发出`filesDropped`信号时，调用当前对象（即this）的addToDB函数，该函数需要一个`QStringList`参数。**连接使用的是Qt的`QueuedConnection`方式**，这意味着函数调用将被放入事件队列中，以便在当前事件处理结束后执行。

值得注意的是，这里使用了一个函数指针`qOverload<QStringList>(&ccViewer::addToDB)`，它指定了要调用的函数的签名。这对于具有多个重载版本的函数非常有用，因为它可以让Qt找到正确的函数版本并进行调用。



至于如何理解其中的:

```c++
qOverload<QStringList>(&ccViewer::addToDB)
```

`qOverload`是Qt提供的一个模板函数，用于指定信号与槽连接中要调用的槽函数的签名，以避免函数重载时的二义性。具体来说，它的语法如下：

```C++
qOverload<T>(&Class::Function)
```

其中，Class是包含该函数的类，Function是要调用的函数名，T则代表该重载函数区别于其他函数的形参类型。

具体来说，`addToDB`函数有两个重载，分别为：

```C++
void ccViewer::addToDB(QStringList filenames)
{
	···
}
```

以及

```C++
void ccViewer::addToDB(ccHObject* entity)
{
	···
}
```

经典的重载函数，名字、返回值相同，以传入的形参不同进行区分

根据语句`qOverload<QStringList>(&ccViewer::addToDB)`，QT可以清楚地知道要调用的是第一个`addToDB`函数（形参类型为`QStringList`），而不会和其他重载函数混淆，保证将信号与正确地槽函数相连接。



# CloudCompare

## 基本架构

```text
CloudCopmare
    ^      ^
    |      |
QCC_IO     QCC_GL
   ^        ^  ^
    \      /    \
     QCC_DB     CC_FBO
       ^
       |
    CC_CORE
```

上图描述了 `CloudCompare` 的几个主要模块和他们之间的依赖关系。

- `CloudCopmare` 是程序本身
- `QCC_IO` 负责点云文件的加载和保存
- `QCC_GL` 负责点云的渲染
- `CC_FBO` 负责实现渲染数据的管理
- `QCC_DB` 负责实现模型数据在内存中的存储管理
- `CC_CORE` 实现了点云相关的数据结构和算法

## 模块介绍

上面这些主要模块中，带有 "Q" 开头的说明这个模块依赖 QT。下面自底向上逐个介绍这些模块。

### CC_CORE

CC_CORE 被作为独立代码库脱离了 CloudCompare 仓库，放在[`CCCoreLib库`](https://github.com/CloudCompare/CCCoreLib)，在 CloudCompare 项目下的 `/libs/qCC_db/extern/CCCoreLib` 目录作为 git 子模块引入。

该部分实现了很多点云处理相关数据结构和算法，例如数据结构 `CCVector`、`DgmOctree` 和`Neighbourhood`等，还有用来描述三维模型的各种 `cloud`、`mesh` 和 `polyline` 类型，算法方面提供了常用的点云算法。

### QCC_DB

该模块在 `/libs/qCC_db` 目录下。

这部分实现了 `cloud`、`mesh` 和 `polyline` 等模型数据在内存中存储和管理功能。

这些模型类全都继承自 `ccHObject` 类型，`ccHobject` 又继承了 `ccDrawableObject`、`ccSeriallzableObject` 和 `ccObject`，分别提供绘制、序列化和元信息查询的接口。

### QCC_IO

该模块在 `/libs/qCC_io` 目录下。

这部分规范了文件输入输出的接口，使用 `FileIOFilter` 作为基类，派生实现不同类型的模型文件的加载和保存。

源码中已经实现了几个常见的文件类型的 `FileIOFilter`，如果想要实现自己的模型文件的加载和保存，可以以插件的形式添加到到 `CloudCompare` 中，继承 `FileIOFilter` 类并实现对应的接口，最后再调用注册函数启用。

### QCC_GL 和 CC_FBO

这俩模块在 `/libs/qCC_glWindow` 和 `/libs/CCFbo` 目录下。

这部分实现了模型数据的渲染，底层用的是 `OpenGL`，实现比较复杂。如果需要拓展新类型的模型或者是自定义渲染效果就需要关注这个模块。

## 二次开发

拓展 CloudCompare 的方式有两种，一种是 UI 界面添加新的组件，另一种是插件化开发。

### UI 功能扩展

UI 拓展就是 QT 信号槽那一套，先打开 `/qCC/ui_templates` 目录，找到想要修改的 ui 文件，然后再实现一下对应的槽函数就可以了。

### 插件扩展

插件拓展除了不能修改 CloudCompare 本身的 UI 以外，可以拓展任意想要的功能，CloudCompare 提供了三种基本类型的插件抽象，分别是 IO 插件、GL 插件和标准插件。

IO 插件是对 `QCC_IO` 模块的拓展，实现自定义文件的加载和保存。

GL 插件是对 `QCC_GL` 和 `CC_FBO` 的拓展，实现自定义的模型渲染或渲染效果。

标准插件则没有上俩个插件的限制，可以拓展任何想要的功能。 

## 代码解析

