---
title: Qt项目的文件结构
date: 2023-03-16 10:50:11
tags: Qt
category: Qt学习
---

之前新建Qt项目看它那个代码，总是感觉怪怪的，直到今天在问ChatGPT关于Qt6和OCC7.6的配合时，它给出了一个Qt+OCC的显示模型的例程，看了这个之后我感觉对Qt程序的创建执行才算理解了一点。

```cpp
#include <QApplication>
#include <QWidget>
#include <QVBoxLayout>
#include <QGraphicsScene>
#include <QGraphicsView>
#include <OpenGl_GraphicDriver.hxx>
#include <V3d_View.hxx>
#include <AIS_InteractiveContext.hxx>
#include <BRepPrimAPI_MakeSphere.hxx>

int main(int argc, char *argv[])
{
    // 初始化 Qt 应用程序
    QApplication app(argc, argv);

    // 创建主窗口
    QWidget window;
    window.setWindowTitle("OCC and Qt Integration");
    window.resize(640, 480);

    // 创建图形场景和视图
    QGraphicsScene scene;
    QGraphicsView view(&scene);
    view.setViewport(new QOpenGLWidget());  // 使用 OpenGL 视口

    // 创建 OCC 视图
    Handle(OpenGl_GraphicDriver) aDriver = new OpenGl_GraphicDriver();
    Handle(V3d_View) aView = new V3d_View(aDriver);
    Handle(AIS_InteractiveContext) aContext = new AIS_InteractiveContext(aView);
    aView->SetContext(aContext);

    // 创建 OCC 对象并将其添加到场景中
    BRepPrimAPI_MakeSphere aSphere(50);
    TopoDS_Shape aShape = aSphere.Shape();
    Handle(AIS_Shape) anAisShape = new AIS_Shape(aShape);
    aContext->Display(anAisShape, Standard_True);
    aContext->UpdateCurrentViewer();

    // 将 OCC 视图绑定到 Qt 视图中
    aView->SetWindow(view.winId());
    aView->MustBeResized();
    view.show();

    // 将 Qt 视图添加到主窗口中
    QVBoxLayout layout;
    layout.addWidget(&view);
    window.setLayout(&layout);
    window.show();

    // 运行 Qt 应用程序
    return app.exec();
}
```

重点不在如何显示OCC模型，而在于该程序是标准的从int main（）主函数来构建程序的写法。从中我们可以加深对Qt代码的真实执行过程的理解。

将上面的代码与下面新建的Qt项目所给出的int main（）比较，可以看到只有寥寥几行代码，当初被下面这几行代码整蒙了，寻思这是干嘛呢，但其实对照上面的代码来分析就比较好读懂了。上面把定义窗口组件的代码直接写在主函数main中，而下面这种其实就是把窗口定义之类的代码写到了类里，这里这个类是OCC_QT，然后`OCC_QT w;`这句其实是调用了该类的默认构造函数，通过构造函数的执行，来实现了窗口的创建等功能。

```cpp
#include "OCC_QT.h"
#include <QtWidgets/QApplication>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    OCC_QT w;
    w.show();
    return a.exec();
}
```

下面来看OCC_QT这个类，先看头文件OCC_QT.h，这里就是类的声明，其中构造函数`OCC_QT(QWidget *parent = nullptr);`

```cpp
#pragma once

#include <QtWidgets/QMainWindow>
#include "ui_OCC_QT.h"

class OCC_QT : public QMainWindow
{
    Q_OBJECT

public:
    OCC_QT(QWidget *parent = nullptr);
    ~OCC_QT();

private:
    Ui::OCC_QTClass ui;
};

```

我们可以看到它引入了一个头文件“ui_OCC_QT.h"，这里面就是窗口组件相关的代码

具体来看“ui_OCC_QT.h"，这里面定义了各种窗口组件的代码，包括页面组件的声明、布局的位置等。

```cpp
/********************************************************************************
** Form generated from reading UI file 'OCC_QT.ui'
**
** Created by: Qt User Interface Compiler version 6.4.0
**
** WARNING! All changes made in this file will be lost when recompiling UI file!
********************************************************************************/

#ifndef UI_OCC_QT_H
#define UI_OCC_QT_H

#include <QtCore/QVariant>
#include <QtWidgets/QApplication>
#include <QtWidgets/QMainWindow>
#include <QtWidgets/QMenuBar>
#include <QtWidgets/QStatusBar>
#include <QtWidgets/QToolBar>
#include <QtWidgets/QWidget>

QT_BEGIN_NAMESPACE

class Ui_OCC_QTClass
{
public:
    QMenuBar *menuBar;
    QToolBar *mainToolBar;
    QWidget *centralWidget;
    QStatusBar *statusBar;

    void setupUi(QMainWindow *OCC_QTClass)
    {
        if (OCC_QTClass->objectName().isEmpty())
            OCC_QTClass->setObjectName("OCC_QTClass");
        OCC_QTClass->resize(600, 400);
        menuBar = new QMenuBar(OCC_QTClass);
        menuBar->setObjectName("menuBar");
        OCC_QTClass->setMenuBar(menuBar);
        mainToolBar = new QToolBar(OCC_QTClass);
        mainToolBar->setObjectName("mainToolBar");
        OCC_QTClass->addToolBar(mainToolBar);
        centralWidget = new QWidget(OCC_QTClass);
        centralWidget->setObjectName("centralWidget");
        OCC_QTClass->setCentralWidget(centralWidget);
        statusBar = new QStatusBar(OCC_QTClass);
        statusBar->setObjectName("statusBar");
        OCC_QTClass->setStatusBar(statusBar);

        retranslateUi(OCC_QTClass);

        QMetaObject::connectSlotsByName(OCC_QTClass);
    } // setupUi

    void retranslateUi(QMainWindow *OCC_QTClass)
    {
        OCC_QTClass->setWindowTitle(QCoreApplication::translate("OCC_QTClass", "OCC_QT", nullptr));
    } // retranslateUi

};

namespace Ui {
    class OCC_QTClass: public Ui_OCC_QTClass {};
} // namespace Ui

QT_END_NAMESPACE

#endif // UI_OCC_QT_H
```

补充一点关于上面部分代码的理解：

```C++
namespace Ui {
    class OCC_QTClass: public Ui_OCC_QTClass {};
} // namespace Ui
```

这段代码声明了一个命名空间Ui，并在里面定义了一个新的类OCC_QTClass来继承上面具体实现功能的类Ui_OCC_QTClass，然后OCC_QT.h中，声明窗口类的时候：`Ui::OCC_QTClass ui;`，用的也是这个新建的OCC_QTClass类，至于为什么要这么干，我猜可能是进一步提高代码的封装性，提高项目的安全性。

最后再来看OCC_QT.cpp，这里面就是OCC_QT类的各种函数功能的具体实现。这里别看这个构造函数就一句话，当时我也懵了一下，寻思这怎么就能把窗口之类的东西都弄出来了？现在懂了，就像上面说的，窗口之类的代码实现实际上都在上面ui_OCC_QT.h里，所以cpp这里的构造函数只需要调用一下setupUi（）函数，把窗口布局的代码运行一下即可。

```cpp
#include "OCC_QT.h"

OCC_QT::OCC_QT(QWidget *parent)
    : QMainWindow(parent)
{
    ui.setupUi(this);
}

OCC_QT::~OCC_QT()
{}

```

分析完这个OCC_QT类，再来看主函数的代码就很好理解了，调用OCC_QT的构造函数将窗口组件都定义好了，之后再使用w.show()函数显示在w这个类中声明与定义的窗口即可。其中这个show()函数我们注意到并没有定义在OCC_QT类中，它应该是继承自QMainWindow的方法。

```cpp
#include "OCC_QT.h"
#include <QtWidgets/QApplication>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    OCC_QT w;
    w.show();
    return a.exec();
}
```

最后大致总结一下新建的这个Qt项目，它在执行时所做的一些工作：

定义了UI界面类Ui_OCC_QTClass，写在“ui_OCC_QT.h”中，其中有窗口各种组件的声明和布局定义，与槽函数的连接也默认写在这里面，又定义了一个新的类OCC_QTCLass继承Ui_OCC_QTClass作为访问接口。定义了窗口类OCC_QT，声明部分写在“OCC_QT.h”里，声明了OCC_QTClass类的对象ui，之后的槽函数声明也写在该文件里；定义部分写在“OCC_QT.cpp”里，构造函数调用ui.setup（）函数对窗口组件进行实现，之后的槽函数定义也写在该文件里。

有了上述这些类的定义，之后就是在主函数中使用，主函数main声明了OCC_QT类的对象w，并调用其构造函数，该构造函数调用OCC_QTClass的实例ui的setup函数，对窗口组件进行声明和定义，即对窗口各组件进行实现。之后再调用OCC_QT的父类QMainWindow继承来的show（）函数将窗口显示出来。



了解了Qt项目的这些结构之后，我们对Qt项目代码的执行过程就有了基本的了解，就可以更好地编写自己的Qt项目。

可以就依赖它给出的这种结构来写，也可以按自己想法来写不按它上面的这种结构，步骤对了就行。

后记：槽函数的声明、定义、与信号的连接等基本步骤见后续的Qt学习笔记，想记录一下两种方式，一种是配合Qt Designer的可视化编程，一种就是纯代码开发的方式。在第一种方式里，想着用上上面说的Qt项目自带的这种文件结果，把OCC_QT.h，OCC_QT.cpp，ui_OCC_QT.h三个文件都用上。在第二中纯代码的方式里，就不要这个ui_OCC_QT.h文件了，毕竟这个文件其实是为了配合Qt Designer可视化编程而存在的，把里面的组件声明、定义等代码都放到外面来。
