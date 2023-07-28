---
title: ccviewer学习笔记
date: 2023-04-19 10:51:00
tags: 
- Qt
- cloudcompare
category: 笔记
---



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

