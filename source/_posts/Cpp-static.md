---
title: C++类的静态成员
date: 2024-01-18 10:26:42
tags: C++
category: 笔记
---



## 对静态成员变量的理解

在类中，定义静态成员变量作为属性，该静态成员变量全局共享。

应当如何理解这个全局共享？是变量名一样就会访问到同一个变量吗？还是怎样？

从静态成员变量的初始化中其实可以看出端倪。

静态成员变量的初始化需要在类外进行，比如自定义一个类A，其成员变量a1为静态成员变量，以`static int a1;` 为例

`a.h`

```C++
class A {
public:
    void seta1(int a1);
    int geta1();
private:
    static int a1;
};
```

那么就需要在a.cpp中，类外对a1进行初始化，注意初始化时要带着变量类型和变量所属的类

`a.cpp`

```c++
#include "a.h"
#include <iostream>
int A::a1 = 0;
void a::seta1(int a1)
{
	this->a1 = a1;
}

int a::geta1() {
	return this->a1;
}
```

这其实就表明`a1`这个变量的生命周期同类A共存，而且是所有的类A

就是说，你先声明一个`A a`，再声明一个`A aa`。

这两个对象，都是类A的对象，它们的成员变量a1是共享的。

改变aa的a1值，就等于改变a的a1值，他俩的a1值是一个东西，绑定的，共享的。是这样的一个共享。

`main.cpp`

```cpp
#include "a.h"
using namespace std;
int main() {
    A a;
    A aa;
    a.seta1(50);
    aa.seta1(100);
    cout<<"a.a1 = "<<a.geta1()<<endl;
    cout<<"aa.a1 = "<<aa.geta1()<<endl;
    return 0;
}
```

输出:

```bash
a.a1 = 100
aa.a1 = 100
```

***



然后就算通过别的类，或是随便其他什么地方，创建了A的对象，来改变对象中a1的值，效果也是一样的。

`b.h`

```cpp
void bar();
```

`b.cpp`

```cpp
#include "a.h"
#include"b.h"
void bar() {
    A obj;
    obj.seta1(100);
}
```

`main.cpp`

```cpp
#include "b.h"
using namespace std;
int main() {
    A a;
    a.seta1(50);
    bar();//调用b.h中的方法
    cout<<"a.a1 = "<<a.geta1()<<endl;
    return 0;
}
```

输出：

```bash
a.a1 = 100
```

上面虽然主函数中的`a.seta1(50);`将a1的值设为了50，但是调用bar()方法，该方法中也声明了一个A的对象obj，也设置了a1的值为100，因为a1为静态成员变量，所以它们数据共享，相当于一个东西，所以最终a1的值就是最后改动的结果：100

***

而在类A的外面的哪个地方，声明一个int a1，类型、变量名一样，这样是不会和类A里的a1共享的，这里的a1，是在它所在作用域的一个新的局部变量。

`main.cpp`

```cpp
#include "a.h"
using namespace std;
int main() {
    int a1;
    A a;
    a.seta1(50);
	cout<<a1<<endl;//警告,使用未初始化的变量
    return 0;
}
```



## 类的静态成员函数

上面说的是其实都是针对类来说的，类中的静态成员变量，下面提一下类中的静态成员函数

静态成员函数是属于类的函数，而不是类的对象实例。它们与特定的对象实例无关，可以直接通过类名来调用，而无需创建类的对象。静态成员函数在类的所有对象实例之间共享。

`myclass.h`

```cpp
class MyClass {
public:
    static int staticMemberVariable;  // 静态成员变量

    static void staticMemberFunction() {  // 静态成员函数
        // 实现代码
    }
};

int MyClass::staticMemberVariable = 0;  // 静态成员变量的定义和初始化

int main() {
    MyClass::staticMemberFunction();  // 调用静态成员函数

    int value = MyClass::staticMemberVariable;  // 访问静态成员变量
}
```

`myclass.cpp`

```cpp
#include "myclass.h"

int MyClass::staticMemberVariable = 0;  // 静态成员变量的定义和初始化

static void staticMemberFunction() {  // 静态成员函数
    ... ... // 实现代码
}
```

静态成员函数的定义和声明与普通成员函数类似，但需要在函数声明和定义中使用 `static` 关键字来标识。

`main.cpp`

```cpp
#include "myclass.h"
int main() {
    MyClass::staticMemberFunction();  // 调用静态成员函数
    int value = MyClass::staticMemberVariable;  // 访问静态成员变量
}
```

可以看到在没有声明`MyClass`类的实例的情况下，可以直接通过范围解析运算符 **::** 对静态成员函数进行访问

顺便一提，可以看到静态成员变量也可以通过这种方式访问，不过前提是该成员变量是`public`的，通常情况下成员变量会设为`private`，所以没法这样直接访问

