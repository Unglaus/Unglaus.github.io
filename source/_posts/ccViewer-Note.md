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


