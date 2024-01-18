---
title: C++中function关键字及lambda表达式
date: 2024-01-16 09:23:44
tags: C++
category: 笔记
---

## function关键字

```C++
#include<functional>
```

### 基本语法

举例说明

```C++
function<int(int)> dp = [&](int i)->int {...};//注意分号;结尾
```

上面是用function关键字定义的lambda表达式，其中`function<int(int)>中int(int)`部分的含义为：

前一个`int`，即紧跟着尖括号“`<`”的`int`表示返回值类型；小括号中的`(int)`表示参数类型。

再举一个例子：

```C++
#include <iostream>
#include <functional>

int add(int a, int b) {
  return a + b;
}

int main() {
  std::function<int(int, int)> add_func = add; // 定义一个函数对象，指向函数add
  std::cout << add_func(2, 3) << std::endl; // 输出 5
  
  return 0;
}
```

`int(int, int)`表示函数的参数列表和返回值类型，其中`int`表示返回值类型，`(int, int)`表示参数列表，表示该函数接受两个`int`类型参数。



### 基本用法

**以下来自ChatGPT**

在C++中，`function`是一个函数对象，它可以像普通函数一样调用。`function`通常用于实现回调函数、函数指针、函数对象等功能。

`function`的用法有以下几种：

- **1、定义函数对象**

可以使用`function`关键字定义一个函数对象，该函数对象可以像普通函数一样调用。例如：

```C++
#include <iostream>
#include <functional>
using namespace std;
int add(int a, int b) {
  return a + b;
}

int main() {
  function<int(int, int)> add_func = add;
  cout << add_func(2, 3) << endl; // 输出 5
  
  return 0;
}
```

在上面的代码中，我们使用`function`定义了一个名为`add_func`的函数对象，该对象接受两个整数参数并返回它们的和。我们将其初始化为指向函数`add`的指针，并使用`add_func`调用该函数。

- **2、定义Lambda表达式**

可以使用`function`关键字定义一个Lambda表达式，该表达式可以像普通函数一样调用。例如：

```C++
#include <iostream>
#include <functional>
using namespace std;
int main() {
  function<int(int, int)> add_func = [](int a, int b) {
    return a + b;
  };
  cout << add_func(2, 3) << endl; // 输出 5
  
  return 0;
}
```

在上面的代码中，我们使用`function`定义了一个名为`add_func`的函数对象，该对象接受两个整数参数并返回它们的和。我们将其初始化为一个Lambda表达式，并使用`add_func`调用该表达式。

- **3、实现回调函数**

可以使用`function`定义一个回调函数，该函数可以作为参数传递给其他函数，并在需要时被调用。例如：

```C++
#include <iostream>
#include <functional>
using namespace std;
void doSomething(int a, int b, std::function<void(int)> callback) {
  int result = a + b;
  callback(result);
}

int main() {
  doSomething(2, 3, [](int result) {
    cout << "The result is: " << result << endl;
  });
  
  return 0;
}
```

在上面的代码中，我们定义了一个函数`doSomething`，该函数接受两个整数参数和一个回调函数作为参数。在函数内部，我们计算两个整数的和，并将结果传递给回调函数。我们在`main`函数中调用`doSomething`函数，并传递一个Lambda表达式作为回调函数，该表达式输出计算结果。

需要注意的是，`function`可以接受任意类型的函数或Lambda表达式作为参数，并可以返回任意类型的值。这使得`function`非常灵活和通用。



## lambda函数（C++11新特性）

lambda 表达式可以说是 c++11 引用的最重要的特性之一， 它定义了一个匿名函数， 可以捕获一定范围的变量在函数内部使用，
 一般有如下语法形式：

```C++
auto func = [capture] (params) opt -> ret { func_body };
```

其中 func 是可以当作 lambda 表达式的名字，作为一个函数使用，capture 是捕获列表，params 是参数表，opt： 不需要可以省略，ret 是返回值类型，func_body 是函数体。
示例：

```C++
auto func1 = [](int a) -> int { return a + 1; };
auto func2 = [](int a) { return a + 2; };
cout << func1(1) << " " << func2(2) << endl;
```

### 捕获列表

| []       | 不捕捉任何变量                                               |
| -------- | ------------------------------------------------------------ |
| [&]      | 捕获外部作用域中所有变量，并作为引用在函数体内使用 (按引用捕获) |
| [=]      | 捕获外部作用域所有变量，在函数内内有个副本使用,拷贝的副本在匿名函数体内部是只读的 |
| [=,&foo] | 按值捕获外部作用域中所有变量，并按照引用捕获外部变量 foo     |
| [bar]    | 按值捕获 bar 变量，同时不捕获其他变量                        |
| [&bar]   | 按引用捕获 bar 变量，同时不捕获其他变量                      |
| [this]   | 捕获当前类中的 this 指针,让 lambda 表达式拥有和当前类成员函数同样的访问权限,如果已经使用了 & 或者 =, 默认添加此选项 |

示例：

```C++
#include <iostream>
#include <functional>
using namespace std;

class Test
{
public:
    void output(int x, int y)
    {
        //auto x1 = [] {return m_number; };                      // error
        auto x2 = [=] {return m_number + x + y; };             // ok
        auto x3 = [&] {return m_number + x + y; };             // ok
        auto x4 = [this] {return m_number; };                  // ok
        //auto x5 = [this] {return m_number + x + y; };          // error
        auto x6 = [this, x, y] {return m_number + x + y; };    // ok
        auto x7 = [this] {return m_number++; };                // ok
    }
    int m_number = 100;
};
```

| x1   | 错误，没有捕获外部变量，不能使用类成员 m_number              |
| ---- | ------------------------------------------------------------ |
| x2   | 正确，以值拷贝的方式捕获所有外部变量                         |
| x3   | 正确，以引用的方式捕获所有外部变量                           |
| x4   | 正确，捕获 this 指针，可访问对象内部成员                     |
| x5   | 错误，捕获 this 指针，可访问类内部成员，没有捕获到变量 x，y，因此不能访问。 |
| x6   | 正确，捕获 this 指针，x，y                                   |
| x7   | 正确，捕获 this 指针，并且可以修改对象内部变量的值           |



示例：

```C++
int main(void)
{
    int a = 10, b = 20;
   // auto f1 = [] {return a; };                        // error
    auto f2 = [&] {return a++; };                     // ok
    auto f3 = [=] {return a; };                       // ok
  //  auto f4 = [=] {return a++; };                     // error
 //   auto f5 = [a] {return a + b; };                   // error
    auto f6 = [a, &b] {return a + (b++); };           // ok
    auto f7 = [=, &b] {return a + (b++); };           // ok

    return 0;
}
```

| f1   | 错误，没有捕获外部变量，因此无法访问变量 a                   |
| ---- | ------------------------------------------------------------ |
| f2   | 正确，使用引用的方式捕获外部变量，可读写                     |
| f3   | 正确，使用值拷贝的方式捕获外部变量，可读                     |
| f4   | 错误，使用值拷贝的方式捕获外部变量，可读不能写               |
| f5   | 错误，使用拷贝的方式捕获了外部变量 a，没有捕获外部变量 b，因此无法访问变量 b |
| f6   | 正确，使用拷贝的方式捕获了外部变量 a，只读，使用引用的方式捕获外部变量 b，可读写 |
| f7   | 正确，使用值拷贝的方式捕获所有外部变量以及 b 的引用，b 可读写，其他只读 |



### 返回值

很多时候，lambda 表达式的返回值是非常明显的，因此在 C++11 中允许省略 lambda 表达式的返回值。

```C++
// 完整的lambda表达式定义
auto f = [](int a) -> int
{
    return a+10;  
};

// 忽略返回值的lambda表达式定义
auto f = [](int a)
{
    return a+10;  
};
```

一般情况下，不指定 lambda 表达式的返回值，编译器会根据 return 语句自动推导返回值的类型，`但需要注意的是 labmda表达式不能通过列表初始化自动推导出返回值类型`。

```c++
// ok，可以自动推导出返回值类型
auto f = [](int i)
{
    return i;
}

// error，不能推导出返回值类型
auto f1 = []()
{
    return {1, 2};	// 基于列表初始化推导返回值，错误
}
```

### 函数本质

使用 lambda 表达式捕获列表捕获外部变量，如果希望去修改按值捕获的外部变量，那么应该如何处理呢？这就需要使用 mutable 选项，`被mutable修改是lambda表达式就算没有参数也要写明参数列表，并且可以去掉按值捕获的外部变量的只读（const）属性。`

```C++
int a = 0;
auto f1 = [=] {return a++; };              // error, 按值捕获外部变量, a是只读的
auto f2 = [=]()mutable {return a++; };     // ok
```

最后再剖析一下为什么通过值拷贝的方式捕获的外部变量是只读的:

lambda表达式的类型在C++11中会被看做是一个带operator()的类，即仿函数。
按照C++标准，lambda表达式的operator()默认是const的，一个const成员函数是无法修改成员变量值的。
mutable 选项的作用就在于取消 operator () 的 const 属性。

因为 lambda 表达式在 C++ 中会被看做是一个仿函数，因此可以使用std::function和std::bind来存储和操作lambda表达式：

```C++
#include <iostream>
#include <functional>
using namespace std;

int main(void)
{
    // 包装可调用函数
    std::function<int(int)> f1 = [](int a) {return a; };
    // 绑定可调用函数
    std::function<int(int)> f2 = bind([](int a) {return a; }, placeholders::_1);

    // 函数调用
    cout << f1(100) << endl;
    cout << f2(200) << endl;
    return 0;
}
```

对于没有捕获任何变量的 lambda 表达式，还可以转换成一个普通的函数指针：

```C++
using func_ptr = int(*)(int);
// 没有捕获任何外部变量的匿名函数
func_ptr f = [](int a)
{
    return a;  
};
// 函数调用
f(1314);
```

