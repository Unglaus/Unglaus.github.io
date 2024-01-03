---
title: C/C++笔记
date: 2022-11-01 21:54:17
tags: 
- C
- C++
category: 笔记
---

# C/C++相关

## 变量声明

如果变量声明在主函数外部，即作为全局变量的时候，其默认是为0；而如果变量声明在函数内部，变量的值是随机的，而不是默认为零，需要进行初始化

```C++
#include<iostream>
using namespace std;

const int N=10;

int a[N];

int main(){
	int b[N];
    for(int i=0;i<N;++i){
        cout<<"a["<<i<<"]:"<<a[i]<<" ";
        cout<<"b["<<i<<"]:"<<b[i]<<endl;
    }
    return 0;
}
```

一次运行的结果如下：

```
a[0]:0 b[0]:8
a[1]:0 b[1]:0
a[2]:0 b[2]:4199705
a[3]:0 b[3]:0
a[4]:0 b[4]:8
a[5]:0 b[5]:0
a[6]:0 b[6]:48
a[7]:0 b[7]:0
a[8]:0 b[8]:15603440
a[9]:0 b[9]:0
```

可以看到作全局变量的a[]，其中所有值都默认为0；而作局部变量的b[]，其中的值是随机赋予的，下一次运行时，其中的值又不一定是什么了，所以对于声明在函数内部的局部变量一定要注意初始化问题，防止由此引发的错误。

**注意：**不是只有数组是这样，只要是变量，都符合上述性质，局部变量的默认值是随机的，全局变量的默认值才是0。

## 关于输入、输出

### **输入**

```c
scanf("%d",&a);//输入整数
//"%d"表示整数int
//"%lf"表示长浮点数double
//"%f"表示浮点数float
//"%s"表示字符串string
//"%c"表示字符char
```

**注意：**scanf ( )是有返回值的，返回值表示成功匹配和赋值的个数（int）

### **输出**

```C
printf("%d\n",a);//输出整数,\n表示输出a之后回车
printf("%d %d",a,b);//输出的两个数之间也会空一格空格，跟"%d %d"保持一致
```

若要使输出保留固定几位小数

```c
printf("%.2lf",a);//".2lf"表示保留两位小数输出double类型的a
```

若想输出固定位数长度的整数，且不够的位补0

```c
printf("%03d",a);//"%03d"表示输出3位整数，不够的位补0，如25如果按"%03d%输出，结果为025
```

如果不加0，只规定位数，则不够的位会用空格补齐

```c
printf("%3d",a);//如25按"%3d"输出，结果为·25(前面的‘·’表示空格，方便看)
```



## 数组操作

**数组初始化**

```c
#include<string.h>
memset(a,0,sizeof(a));//把数组a清零
```

**数组间复制**

将数组a复制k个元素到数组b中

```c
#include<string.h>
memcpy(b,a,sizeof(int)*k);//这里就当a和b都是int数组
```

同理可知若两个都是double数组，则

```c
memcpy(b,a,sizeof(double)*k);
```

把数组a全部复制到数组b中

```
memcpy(b,a,sizeof(a));
```



## 字符数组

**输入字符数组**

```c
char s[20];
scanf("%s",s);//注意这里的s前面没有“&”
```

上述语句会将读入的字符串存到字符数组s中，遇到空格、TAB和回车会终止读入

**输入字符**

```c
scanf("%s",&s[i]);//这时候前面要加“&”
```

**字符数组的复制**

```c
#include<string.h>
char a[10],b[10];
strcpy(a,b);//将b字符串复制到a
```

**字符串的比较**

```
strcmp(s1,s2);
```

字符串大小的比较是以ASCII 码表上的顺序来决定，此顺序亦为字符的值。strcmp()首先将s1 第一个字符值减去s2 第一个字符值，若差值为0 则再继续比较下个字符，若差值不为0 则将差值返回。

```c
#include <string.h>
main(){
    char *a = "aBcDeF";
    char *b = "AbCdEf";
    char *c = "aacdef";
    char *d = "aBcDeF";
    printf("strcmp(a, b) : %d\n", strcmp(a, b));
    printf("strcmp(a, c) : %d\n", strcmp(a, c));
    printf("strcmp(a, d) : %d\n", strcmp(a, d)); 
    }
```

输出结果如下：

```
strcmp(a, b) : 32
strcmp(a, c) :-31
strcmp(a, d) : 0
```



**字符串的连接**

```c
#include<string.h>
char a[10],b[10];
strcat(a,b);//将字符串a的内容接到b字符串之后
```

注意b字符串大小为10，这个大小需要能够容纳连接后的总字符串长度

连接的过程相当于将a中的字符串顺序填到b字符串后的空余位置

如a[10]="aaa"; b[10]="bbb"， 连接后的结果为b[10]="bbbaaa"



**把信息输出到字符串**

```c
int a=65,b=97;
char buf[20];
sprintf(buf,"%d%d",a,b);//把a、b两个数格式化输出到字符数组buf中
```

“%d”部分根据要输出到buf中的内容来定，输字符char就是“%c”，字符串string就是“%s”，都一样的。

最重要的这是格式化输出到buf中，buf中存的信息为“6597”，即buf[0]='6'; buf[1]='5'; buf[2]='9'; buf[3]='7' 。

而不会发生强制类型转换，将a和b所对应ASCII码的字符存入，比如：

```c
int a=65;
char c[10];
*c=a;
```

这种的就会出现强制类型转换，可能是想把65存到c数组中，但实际会发生强制类型转换，将65对应的ASCII码“A”，存到c数组的第一个位置，即c[0]='A'



**求数组实际长度**

像上面那样实际buf声明了20个字节大小，实际并没有全部用完，如果直接要求输出buf中20个字节的内容会出现错误，这时就需要判断buf的实际使用大小

需要用到的函数为

```c
strlen(buf);
```

举例：

```c
for(int i=0;i<strlen(buf);++i)
{
    cout<<buf[i]<<" ";
}
```

这样buf中没有用到的部分不会被要去输出，避免出错



**输入字符串**

使用getchar()函数

```c
int c;
while((c=getchar())!=EOF)//EOF是一个特殊的结束标志
{
	printf("%c",c);
}
```



## 运算符重载

**（详见《C++ Primer》P490）**

重载运算符一般是为了方便直接操作自定义的结构体、类，所以现在这里定义一个结构体，方便下面举例

```c++
struct Point{
    int x,y;
    Point(int x=0,int y=0):x(x),y(y){}//构造函数，默认值0
};
```



**算术操作符重载**

举例：

```c++
Point operator + (const Point &A,const Point &B){
    return Point(A.x+B.x,A.y+B.y);
}
```

现在可以直接操作两个Point类型的变量进行加法运算，运算的规则即上面加法所定义的规则

**输出运算符重载**

输出运算符的第一个形参是一个非常量ostream对象的引用；第二个形参是一个常量的引用，该常量是我们想要打印的类类型。

举例：

```c++
ostream& operator << (ostream &out, const Point &p){
    cout<<"("<<p.x<<","<<p.y<<")";//用out装相应打印的内容，再将out返回
    return out;
}
```

这是我们便可以直接输出结构的内容，输出的形式就是我们上述定义的形式

**上述重载的使用举例：**

```c++
int main(){
    Point a,b(1,2);
    a.x=3;//a.y没有定义,默认为0
    cout << a + b << endl;//先使用了重载的Point加法运算，再用了重载的Point输出运算
    return 0;
}
```

得到的结果为：

```
(4,2)
```

## 关于构造函数

### 成员初始化列表

```C++
class MyClass {
public:
  MyClass(int a, int b) : member_a(a), member_b(b) {}
private:
  int member_a;
  int member_b;
};
```

在这个例子中，构造函数`MyClass(int a, int b)`中使用了成员初始化列表来初始化`member_a`和`member_b`成员变量。成员初始化列表的语法是在构造函数参数列表后面放置一个冒号，然后列出所有要初始化的成员变量和它们的初始值，每个成员变量和初始值之间用逗号分隔。在本例中，`member_a`被初始化为`a`，`member_b`被初始化为`b`。

使用成员初始化列表的主要优点是，它可以提高代码的效率。如果成员变量使用赋值语句而不是成员初始化列表来初始化，那么它们将在对象构造后被初始化，这可能会导致不必要的内存分配和赋值操作。使用成员初始化列表可以避免这种情况，因为它们可以在对象构造期间直接初始化成员变量。

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

## 模板

**函数模板**

```C++
template<typename T>
T sum(T *begin , T *end){
    T *p=begin;
    T ans = 0;
    for(T *p= begin ; p != end; p++){
        ans = ans + *p;
    }
    return ans;
}
```

这个函数模板的作用是求数组的和，使用时直接传参数使用即可，会根据所传参数的类型自动将上述的“T"代换成对应的类型

```C++
int main{
	double a[] = {1.1 , 2.2 , 3.3 , 4.4};
    cout << sum(a,a+4)<<endl;
    Point b[] = {Point(1,2) , Point(3,4) , Point(5,6) , Point(7,8)};
    cout << sum(b,b+4);
    return 0; 
}
```

**结构体模板**

```c++
template<typename T>
struct Point{
    T x,y;
    Point(T x=0,T y=0):x(x),y(y){}
};
```

这时在使用Point模板的时候需要主动声明模板中的“T"具体的类型，具体的用法如下：

```c++
int main{
	Point<int> a(1,2),b(3,4);
    Point<double> c(1.1,2.2),d(3.3,4.4);
    return 0;
}
```



## 类

### 访问控制

- `private`：私有
- `public`：公有
- `protected`：保护

```C++
class Test{
public:
    int a=1;
private:
    int b=2;
protected:
    int c=3;
}
int main(){
    Test t;
    cout<<t.a<<endl;//ok!public,对象可以访问
    cout<<t.b<<endl;//no!private,对象不可访问
    cout<<t.c<<endl;//no!protected,对象不可访问
    return 0;
}
```

### 继承

- `public`：公有继承，父类中**公有成员**和**保护成员**在子类中访问属性不变，**私有成员**在子类中不可直接访问

- `private`：私有继承，父类中**公有成员**和**保护成员**在子类中以私有成员身份出现，**私有成员**在子类中不可直接访问；私有继承使得子类进一步继续派生的情况下，原本父类的成员无法再直接发挥作用，因为它们对进一步派生出的子类而言已经是不可直接访问的私有成员
- `protected`：保护继承，父类中**公有成员**和**保护成员**在子类中以保护成员身份出现，**私有成员**在子类中不可直接访问

### 派生类的构造函数

```c++
#include<iostream>
using namespace std;

class Base1{
public:
    Base1(int i){
        cout<<"Base1 "<<i<<endl;
        a=i;
    }
    int getnum1(){
        return a;
    }
private:
    int a;
};
class Base2{
public:
    Base2(int i){
        cout<<"Base2 "<<i<<endl;
        b=i;
    }
    int getnum2(){
        return b;
    }
private:
    int b;
};

class Base3{
public:
    Base3(){cout<<"Base3 *"<<endl;}//Base3构造函数无参数，无须赋值，初始化时会自动调用该构造
    int getnum3(){
        return c;
    }
private:
    int c=99;
};

class Derived:public Base2,public Base1,public Base3{//赋值时按继承顺序赋值，先Base2，后Base1，最后Base3
public:
    Derived(int a,int b,int c ,int d):Base1(a),member2(d),member1(c),Base2(b){}//赋值顺序见上下两行注释(注意b和d别看岔了)
    int getnumD1(){
        return member1.getnum1();
    }
    int getnumD2(){
        return member2.getnum2();
    }
    int getnumD3(){
        return member3.getnum3();
    }
private:
    Base1 member1;//赋值时按照声明顺序赋值，先member1，后member2，最后member3
    Base2 member2;
    Base3 member3;
};

int main(){
    Derived obj(1,2,3,4);
    cout<<obj.getnumD1()<<endl;//子类使用父类做成员时，能够理所当然使用父类的访问函数，访问父类类型的私有成员
    cout<<obj.getnumD2()<<endl;
    cout<<obj.getnumD3()<<endl;
    cout<<obj.getnum1()<<endl;//子类可以直接通过父类的访问函数，访问初始化之后的父类私有成员
    cout<<obj.getnum2()<<endl;
    cout<<obj.getnum3()<<endl;
    return 0;
}
```

结果展示：

```C
Base2 2
Base1 1
Base3 *
Base1 3
Base2 4
Base3 *
3
4
99
1
2
99
```

**说明：**

关于继承，不要忘了**父类的私有成员也会被继承过来**，只是子类不能直接调用，需要通过父类的方法来调用。

C++11标准中，子类能够从直接父类中继承构造函数并使用（注意只有直接父类才行）。所以，在子类的构造过程中：

`Base1(a)`和`Base2(b)`实际是在子类`Derived`中调用父类`Base1`和`Base2`的构造函数，来对父类继承过来的私有成员`a`、`b`进行初始化。要想访问它们，也要使用父类继承过来的方法才行，即`obj.getnum1()`、`obj.getnum2()`

至于`number1(c)`、`nmuber2(d)`的初始化，它们是`Base1`和`Base2`类型的实例化对象，所以它们的相关操作就是按类`Base1`和类`Base2`中的定义来执行的(按Base类中的构造函数初始化、调用方法之类的)。

关于`Base3()`和`number3()`的初始化，因为它们都有无参构造函数，所以在不传参的时候会默认调用它们的无参构造函数进行舒适化。

最后是关于初始化的顺序，或者说调用构造函数构造的顺序，实现构造基类`Base1-3`，再构造子类的对象`numbe1-3`。

其中基类的构造顺序按照继承时顺序来构造，继承顺序为：`class Derived:public Base2,public Base1,public Base3`，所以基类构造时的顺序为：`Base2()`、`Base1()`、`Base3()`。

子类的对象的构造顺序就按照对象声明时的顺序来，声明顺序为`Base1 number1;Base2 number2;Base3 number3;`所以子类的对象构造顺序为`number1()`、`number2()`、`number3()`。

另外补充一点：**如果有虚基类，虚基类的构造还要排在基类的构造之前**。如下例：

```c++
#include "iostream.h"
class OBJ1
{
    public:
    OBJ1(){cout<<"OBJ"<<endl;}
}
class OBJ2
{
    public:
    OBJ2(){cout<<"OBJ2"<<endl;}
}
class BASE1
{
    public:
    BASE1(){cout<<"BASE1"<<endl;}
}
class BASE2
{
    public:
    BASE2(){cout<<"BASE2"<<endl;}
}
class BASE3
{
    public:
    BASE3(){cout<<"BASE3"<<endl;}
}
 
class BASE4
{
    public:
    BASE4(){cout<<"BASE4"<<endl;}
}
class DERIVER :public BASE1,vitural public BASE2
              public BASE3,virtual public BASE4
{
    public:
    DERIVER():BASE4(),BASE3(),BASE2(),BASE1(),obj2(),obj1(){cout<<"DERIVER"<<endl;}
    protect:
    OBJ1 obj1;
    OBJ2 obj2;
}
/*output
    BASE2
    BASE4
    BASE1
    BASE3
    OBJ1
    OBJ2
    DRIVER
*/
```

- DERIVER的虚基类BASE2和BASE4最先构造，所以先输出了BASE2和BASE4，尽管它们在DERIVER类中的顺序不在最前面。
- 然后在构造DERIVER的非虚基类，虽然它们排在前面，但是要优先构造虚基类，所以放在了虚基类后面。
- 再构造DERIVER的对象obj1和obj2.它们以类定义时，数据成员排在前面的先构造；
- 最后构造DERIVER本身。





### 抽象类实现多态

抽象类的作用就是为后续的派生类提供了一个相当于“标准”之类的东西，派生类对抽象类的中的纯虚函数进行实现，之后定义**基类指针，指向子类**，然后通过这个指针访问函数时，会根据指针指向的类来具体访问指定类的函数，实现多态

```C++
#include<iostream>
#include<string>
using namespace std;

class Shape{//抽象类
public:
    virtual float getArea()=0;//纯虚函数，获得面积
    virtual string getName()=0;//纯虚函数，获得图形名称
};

class Circle:public Shape{//Circle子类，继承自Shape
public:
    Circle(float r):m_r(r){}
    virtual float getArea(){
        return 3.14*m_r*m_r;
    }
    virtual string getName(){
        return "Circle";
    }
private:
    float m_r;
};

class Rectangle:public Shape{//Rectangle子类，继承自Shape
public:
    Rectangle(float w,float h):m_w(w),m_h(h){}
    virtual float getArea(){
        return m_w*m_h;
    }
    virtual string getName(){
        return "Rectangle";
    }
private:
    float m_w,m_h;
};
int main(){
    Shape* shape=NULL;//定义一个空的基类指针
    shape=new Circle(5);//基类指针指向子类对象
    cout<<shape->getName()<<"'s area:"<<shape->getArea()<<endl;
    delete shape;//释放Circle对象所占内存，但指针仍然存在，需要注意的是现在该指针为野指针，使用前一定要重新赋值

    shape=new Rectangle(8,9);//基类指针指向新的子类对象
    cout<<shape->getName()<<"'s area:"<<shape->getArea()<<endl;

    return 0;
}
```

**运行结果：**

```C++
Circle's area:78.5
Rectangle's area:72
```

通过上例，可以看到，针对基类指针指向的不同子类对象，调用相同函数时，相同语句分别实现了不同的功能，分别对应了各自子类的方法，实现了多态。

## auto

针对比较长的变量类型时可以直接写成auto，C++会自动判断变量的类型，将auto替换成对应的变量类型

就比如对vector进行遍历操作时

```c++
for(vector<int>::iterator it=vec.begin(); it!=vec.end(); it++){
    cout<<*it<<endl;
}
//此时就可以直接将"vector<int>::iterator"直接替换为auto
for(auto it=vec.begin();it!=vec.end();it++){
    cout<<*it<<endl;
}
```




## 顺序容器


### string

```C++
#include<string>
```

#### **常用函数**

- `size()/length()` ：返回字符串长度

- `empty()` ：判断字符串是否为空

- `clear()` ：清空字符串
- `find(string s)`：返回子串s在母串中的初始位置

- `substr(size_t pos = 0, size_t len = npos)` ：返回子串，其中第一个参数pos表示子串起始下标，第二个参数表示子串长度
- `c_str()`：返回字符串所在字符数组的起始地址，主要针对printf用的，printf无法直接输出string类型，只能输出字符数组类型的字符串char[]

```c++
int main ()
{
	string str="We think in generalities, but we live in details.";

	string str2 = str.substr (3,5); // 起始坐标为3,子串长度为5,得到"think"
	size_t pos = str.find("live"); // 返回子串"live"在str中的初始位置
	string str3 = str.substr (pos); //缺省方式调用substr函数,第二个参数len默认为npos,表示字符串长度最大值.即得到从"live"到字符串结束的子串
	cout << str2 << '\n' << str3 << '\n';
return 0;
}
```

输出结果为：

```
think 
live in details.
```



### vector

```c++
#include<vector>
```

支持比较运算，按字典算

#### **构造函数**

- `vector()`：创建一个空vector
- `vector(int nSize)`：创建一个vector，元素个数为nSize
- `vector(int nSize,const T &t)`：创建一个vector，元素个数为nSize，且值均为t
- `vector(const vector&)`：复制构造函数
- `vector(begin,end)`：复制[begin,end)区间内另一个数组的元素到vector中（注意区间左闭右开）

用法举例：

```c++
//创建一个空vector
vector<int> v1;

//创建了一个元素个数为n的vector
int n;
cin>>n;
vector<int> v2(n);//其中这n个元素默认值都为0，此时push_back(x)会在这n个0之后添加x

//创建了一个元素个数为n的vector，其中n个元素值都为5
vector<int> v3(n,5);//此时push_back(x)会接着在这n个5之后添加x

//复制构造函数
vector<int> v4(v3);//将v3复制给了v4

//复制区间[begin,end)区间内另一个数组的元素到vector中
int s[] = {1,6,3,2,5};
vector<int> vec(s, s+5);//s+5指向的是s[]中最后一个元素的后一个位置
//如果用vec(s,s+4)则只能将1,6,3,2这四个数赋给vec

```

#### **常用函数**

- `size()`：返回向量中元素的个数
- `empty()`：向量为空则返回true
- `clear()`：清空向量中的所有元素
- `front()`：返回第一个元素的引用
- `back()`：返回最后一个元素的引用
- `begin()`：返回指向向量第一个元素的迭代器
- `end()`：返回指向向量最后一个元素的后一个元素的迭代器
- `push_back()`：向量尾部增加一个元素
- `emplace_back()`：与push_back()相似，向尾部增加一个元素，但省去一次移动或拷贝操作，相对高效一点
- `pop_back()`：删除向量中最后一个元素

对于vector排序，可以使用sort函数，sort函数默认升序排序（从小到大）。

使用sort对vector排序时，从小到大排就用vec.begin()和vec.end()

如果要从大到小排，就用vec.rbegin()和vec.rend()

```c++
int main(){
    int s[] = {1,6,3,2,5};
    vector<int> vec(s, s+5);//初始化vector，将s[]中的内容赋给vec<int>
    cout<<*vec.begin()<<endl;   //指向第一个元素
    cout<<*vec.end()<<endl;     //指向最后一个元素的后一个位置
    cout<<*vec.rbegin()<<endl;  //reverse begin  指向最后一个元素
    cout<<*vec.rend()<<endl;    //指向第一个元素的前一个元素
    
    //正向排序 即按照从小到大的顺序排序
    sort(vec.begin(), vec.end());
    //顺序访问
    for(vector<int>::iterator it=vec.begin(); it!=vec.end(); it++){
        cout<<*it<<" ";
    }
    cout<<endl;

    //逆向排序 即按照从大到小的顺序进行排序
    sort(vec.rbegin(), vec.rend());
    //顺序访问
    for(vector<int>::iterator it=vec.begin(); it!=vec.end(); it++){
        cout<<*it<<" ";
    }
    cout<<endl;

}
```

##### push_back()

```C++
vector<vector<int>> res;
res.push_back({1,3});
```

上面这种大括号的`push_back()`相当于直接添加了一个`vector<int>`类型数据

即向空的二维数组res中添加了一个一维数组[1,3]

res的变化：`[] -> [[1,3]]`



##### 二维数组初始化

```C++
vector<vector<int>> res={{1,2},{3,4}};
res.push_back({5,6});
```

顺便提一下使用vector构造的二维数组的初始化，如上所示，用大括号分隔来进行数据的初始化

构造的二维数组res内容为：`[[1,2],[3,4]]`

向其后插入一个一维数组`[5,6]`，res的变化为：

`[[1,2],[3,4]] -> [[1,2],[3,4],[5,6]]`



### list

和`vector`基本一致，要注意的是`list`的内部存储逻辑是**双向链表**



### stack

```c++
#include<stack>
```

#### **构造函数**

```C++
stack<T> sta;
```

#### **常用函数**

- `size()`：返回栈的长度（元素个数）
- `empty()`：判断栈是否为空
- `push()`：向栈顶插入一个元素（入栈）
- `pop()`：弹出栈顶元素（出栈）
- `top()`：返回栈顶元素



### queue

```
#include<queue>
```

####  **构造函数**

```c++
queue<T> que;
```

#### **常用函数**

- `size()`：返回队列长度（元素个数）
- `empty()`：判断队列是否为空
- `push()`：向队尾插入一个元素（入队）
- `pop()`：弹出队头元素（出队）
- `front()`：返回队头元素
- `back()`：返回队尾元素



### dequeue

```c++
#include<queue>
```

#### **构造函数**

```c++
deque<T> dq;
```

#### **常用函数**

- `size()`：返回双端队列长度（元素个数）
- `empty()`：判读双端队列是否为空
- `clear()`：清空双端队列
- `front()/back()`：返回队头/队尾元素
- `push_back()/pop_back()`：向队尾添加元素/从队尾弹出元素
- `push_front()/pop_front()`：向队头添加元素/从队头弹出元素
- `begin()`：返回指向队中对一个元素的迭代器
- `end()`：返回指向队列最后一个元素的后一个元素的迭代器（past-the-end，是个理论上的元素）



### priority_queue

```C++
#include<queue>
```

#### **常用函数**

- `empty()`：队列为空，返回true
- `top()`：返回队顶元素
- `pop()`：删除队顶元素
- `push()`：插入一个元素（根据规则自动排序）
- `size()`：返回优先队列中拥有的元素个数

#### 定义

```c++
template<
    class T,
    class Container = std::vector<T>,
    class Compare = std::less<typename Container::value_type>
> class priority_queue;
```

| **参数**  | **描述**                                                     | **默认值** |
| --------- | ------------------------------------------------------------ | ---------- |
| T         | 优先队列中存放的数据类型                                     |            |
| Container | 用于实现优先队列（潜在）的容器类型                           | vector\<T> |
| Compare   | 比较函数，用于判断一个元素是否小于另一个元素。如果 Compare(x,y) 为真，则 x 小于 y。Q.top()  返回的元素是优先级队列中最大的元素。也就是说，它的属性是，对于优先级队列中的每个其他元素 x，Compare(Q.top(), x) 为  false。 | less\<T>   |

- Container：必须是用数组实现的容器，如vector、deque，但不能用list。STL中默认使用vector
- Compare：比较方式默认使用less\<T>，operator < (小于号)
- 如果把后面两个参数缺省，优先队列使用默认参数，为大根堆，队顶元素最大

```c++
priority_queue<int> que;
//等价于
priority_queue<int,vector<int>,less<int> > que;
//编译器比较旧两个将括号中间加空格，保险起见，直接加空格为好，防止识别成右移">>"
```



其中less\<T>为仿函数，定义如下：

```c++
// TEMPLATE STRUCT less
template<class _Ty> 
struct less : public binary_function<_Ty, _Ty, bool>
{	// functor for operator<
	bool operator()(const _Ty& _Left, const _Ty& _Right) const
	{	// apply operator< to operands
		return (_Left < _Right);
	}
};
```

less\<T>使用的比较规则是基于 <（小于号）的，所以当priority_queue是基于less比较规则的时候，我们可以重载 <（小于号）来实现自定义类型变量的比较



#### 更改比较函数——仿函数greater\<T>

上面已经说过默认的比较规则less\<T>，由此实现了大根堆的优先队列；STL还定义了与less\<T>相对的仿函数greater\<T>，将priority_queue的第三个参数，即比较规则改为greater\<T>即可实现小根堆。

```c++
priority_queue<int ,vector<int> ,geater<int> > que;
```

其中greater\<T>的定义如下：

```c++
// TEMPLATE STRUCT greater
template<class _Ty>
struct greater : public binary_function<_Ty, _Ty, bool>
{	// functor for operator>
	bool operator()(const _Ty& _Left, const _Ty& _Right) const
	{	// apply operator> to operands
		return (_Left > _Right);
	}
};
```

可以看到相较于less\<T>，greater\<T>的比较规则是基于 >（大于号）的，所以如果要在基于greater\<T>的比较规则下实现自定义类型变量的比较，需要重载 >（大于号）。

#### 自定义类型——大顶堆

STL中的仿函数less\<T>和greater\<T>的使用范围仅限于基本类型，当使用我们自定义的数据类型时，我们需要自定义比较规则。

- **重载运算符 < **

为什么要重载 <（小于号）而不是 >（大于号），原因在于此时我们的声明形式通常是将后面两个参数缺省的，也就是此时会默认使用仿函数less\<T>，而less中的比较使用的是 <（小于号）。如果想要重载 >（大于号），还需要在声明priority_queue时注明剩下的两个参数，并将第三个参数设置为greater\<T>，所以完全不必如此自找麻烦，直接重载 <（小于号）即可。

```c++
// 重载 < 运算符，实现大顶堆
//（堆顶元素：先根据x，选择x最大的元素；若两个元素的x值相同，再根据y，选择两者中y较大的元素） 
bool operator<(My_Type a,My_Type b)
{
    // 定义排序规则 
    if(a.x==b.x) return a.y<b.y;
    return a.x<b.x; 
}
// 定义优先队列
priority_queue<My_Type> que;//缺省声明，默认使用less<T> 
```

- **自定义仿函数**

从priority_queue的定义中已经知道，它进行排序需要依靠其第三个参数定义的比较规则，而这些比较规则用的是仿函数，所以除了重载仿函数使用的比较运算符，我们可以直接自己写一套比较规则，也就是自定义一个仿函数，来实现我们需要的自定义类型变量的比较

```c++
// 仿函数，实现大顶堆 
struct cmp
{
    // 定义排序规则 
    bool operator() (My_Type a,My_Type b )
    { 
        if(a.x==b.x)return a.y<b.y;
        return a.x<b.x; 
    }
}; 
// 定义优先队列
priority_queue<My_Type,vector<My_Type>,cmp>que;
```



#### 自定义类型——小顶堆

跟自定义类型的大顶堆同理，只需要改变部分细节即可

- **重载运算符 < **

```c++
// 重载 < 运算符，实现小顶堆 
bool operator<(My_Type a,My_Type b)
{
    // 定义排序规则 
    if(a.x==b.x) return a.y>b.y;
    return a.x>b.x; 
}
```

- **自定义仿函数**

```c++
// 仿函数，实现小顶堆 
struct cmp
{
    // 定义排序规则 
    bool operator() (My_Type a,My_Type b )
    { 
        if(a.x==b.x)return a.y>b.y;
        return a.x>b.x; 
    }
}; 
```



## 关联容器

### pair

```c++
#include<utility>
```

**类模板：**`template<class T1,class T2> struct pair`

**参数：**T1表示第一个值得数值类型，T2是第二个值得参数类型

**功能：** **pair**将一对值**（t1，t2）**组合成一个值，这一对值可以具有不同数据类型，分别通过pair的成员函数**first**和**second**访问

#### **构造函数**

```c++
pair<T1,T2> p1;//创建一个空pair对象
pair<T1,T2> p2(v1,v2);//创建一个pair对象,p2.first=v1,p2.second=v2
```

#### **常用操作**

- `make_pair(v1,v2)`：以v1和v2的值创建一个新pair对象，元素类型分别为v1和v2的变量类型

```c++
auto p=make_pair(v1,v2);
```

- `p.first`：返回p中第一个元素
- `p.second`：返回p中第二个元素（注意这两个是pair的成员，使用时不要加括号）
- `p1 < p2`：两个pair对象间的小于运算，其定义遵循字典次序：如 p1.first < p2.first 或者 !(p2.first < p1.first) && (p1.second < p2.second) 则返回true
- `p1==p2`：如果两个对象的first和second依次相等，则这两个对象相等



### map/multimap

```c++
#include<map>
```

#### map定义

```c++
template< 
	class Key,                                     // 指定键（key）的类型
    class T,                                       // 指定值（value）的类型
    class Compare = less<Key>,                     // 指定排序规则
    class Alloc = allocator<pair<const Key,T> >    // 指定分配器对象的类型
> class map;
```

| 参数    | 描述                  | 默认值      |
| ------- | --------------------- | ----------- |
| key     | 指定键（key）的类型   |             |
| T       | 指定值（value）的类型 |             |
| Compare | 指定排序规则          | less\<key>  |
| Alloc   | 指定分配器对象的类型  | pair<key,T> |

- 通常情况在声明map类型变量是只设定前两个参数的值
- 第三个参数默认使用less\<key>规则排序，即会按照key值的大小进行升序排序，可根据自身需要改变该参数（自定义仿函数）或者重载 <（小于号）
- 第四个参数基本不会用到，其默认为pair<key,T>，即map中每个元素是一个pair对象

#### map和multimap的区别

`map`中的一个关键字`key`只能出现一次，而`multimap`中的，一个关键字`key`可以出现多次

#### 构造函数

```c++
map<int,int> m;//简单举个例子
```



#### 常用函数

- `size()`
- `empty()`
- `clear()`
- `begin()/end()`
- `++/--`：支持迭代器的`++`或`--`操作
- `insert()`：向map中插入键值对，元素类型应为pair类型

```c++
map<string,int> m;
pair<string,int> p;
//有现成pair类型
m.insert(p);
//没有现成pair类型，可以在insert参数列表中创建一个pair
m.insert({"word",1});
m.insert(make_pair("word",1));
m.insert(pair<string,int>("word",1));
m.insert(map<string,int>::value_type("word",1));//value_type是map中的类型别名，在这里相当于pair<string,int>，一般谁这么写啊...
```

-  `erase()`：删除元素

| 具体操作       | 描述                                                         |
| -------------- | ------------------------------------------------------------ |
| `c.erase(k)`   | 从c中删除每个关键字为k的元素，返回一个size_type值，指出删除的元素的个数 |
| `c.erase(p)`   | 从c中删除迭代器p指定的元素。p必须指向c中一个真实元素，不能使`c.end()`。返回一个指向p之后元素的迭代器，若p指向c中的尾元素，则返回`c.end()` |
| `c.erase(b,e)` | 删除迭代器对b和e所表示的范围中的元素。返回e                  |

- `operator[]`：map容器重载了 [] 运算符，只要知道 map 容器中某个键值对的键的值，就可以向获取数组中元素那样，通过键直接获取对应的值。
- 注意`multimap`并不支持下标操作，毕竟`multimap`中相同关键字可以出现多次

```C++
c[k];//返回关键字为k的元素(返回的是key对应的value)，如果k不在c中，添加一个关键字为k的元素，对其进行值初始化
c.at(k);//访问关键字为k的元素(也能返回key对应的value)，带参数检查；若k不在c中，抛出一个out_of_range异常
```

- `find(k)`：在 map 容器中查找键为 key 的键值对，如果成功找到，则返回指向该键值对的双向迭代器；反之，则返回和 end() 方法一样的迭代器。另外，如果 map 容器用 const 限定，则该方法返回的是 const 类型的双向迭代器。

```c++
//比较find()和下标操作可以看出，下标操作在没有找到指定key值得元素的时，会自动添加一个键值为key，value默认为0的元素;find()则不会改变map
//所以在不想改变map的情况下，想判断一个元素是否存在应使用find()而不是下标寻找
//当然如果肯定key值对应的元素存在，就是要用下标来找当然没问题
```

- `count(k)`：返回关键字等于k的元素的数量。对于不允许重复关键字的容器，返回值永远是0或1
- `lower_bound(k)`：返回一个迭代器，指向第一个关键字不小于k的元素
- `upper_bound(k)`：返回一个迭代器，指向第一个关键字大于k的元素



### set/multiset

```C++
#include<set>
```

#### set模板定义

```C++
template < 
	class T,                        // 键 key 和值 value 的类型
    class Compare = less<T>,        // 指定 set 容器内部的排序规则
    class Alloc = allocator<T>      // 指定分配器对象的类型
> class set;
```

- `set`和`map`相似，里面存储的也是键值对，但是`set`中键`key`和值`value`的数值要是相等的，因此在声明时只需指定一个变量类型，作为`key`和`value`共同的类型
- `set`也默认使用`less<T>`的排序规则
- 参数三默认的分配器类型是？

#### set和multiset的区别

`multiset` 容器和 `set` 容器唯一的差别在于，`multiset` 容器允许存储多个值相同的元素，而 `set` 容器中只能存储互不相同的元素。

#### 常用操作

与`map/multimap`基本一致，参考`map/multimap`部分即可



### unordered_set, unordered_map, unordered_multiset, unordered_multimap

- 上述容器的无序版本，不会对存储的元素进行排序
- 相关的操作也和上述关联容器形似
- 会有一些特定的函数使用不了，比如`lower_bound(k)/upper_bound(k)`这类牵扯到比较大小的函数
- 注意这些容器使用的存储逻辑是**哈希表**，不支持迭代器的`++`或`--`操作



### bitset

**压位：**用于处理二进制位集合操作

```c++
#include <bitset>
```

#### 构造函数

- ```C++
  bitset<n> b;//b有n位;每一位均为0。
  ```

- ```c++
  bitset<n> b(u);//b是unsigned long long值u的低n位的拷贝。若n大于unsigned long long的大小，则b中超出的高位部分全置为0。
  ```

- ```C++
  bitset<n> b(s,pos,m,zero,one);//b是string s从位置pos开始m个字符的拷贝。
                                //s只能包含字符zero或one，如果s含有其他字符，构造函数抛出异常invalid_argument。
                                //pos默认为0，m默认为string::npos，zero默认为‘0’，one默认为‘1’。
  ```

- ```C++
  bitset<n> b(cp,pos,m,zero,one);//同上一个构造函数相同，但从cp指向的字符数组中拷贝字符
                                 //如果未提供m，则cp必须指向一个C风格字符串。如果提供了m，则从cp开始必须至少有m个zero或one字符。
  ```



#### 常用函数

```C++
bitset<n> b;
```

- `b.count()`： 返回有多少个1
- `b.any()` ：判断是否至少有一个1
- `b.all()`：判断是否全为1
- `b.none()` ：判断是否全为0
- `b.size()`：返回b的位数
- `b.set()` ：把所有位置成1
- `b.set(k, v)`： 将第k位变成v
- `b.reset()` ：把所有位变成0
- `b.reset(k)` ：把第k位复位（变成0） 
- `b.flip()` ：把所有位取反
- `b.flip(k)` ：把第k位取反



## C++函数的使用

### sort

```C++
#include <algorithm>
```

#### 用法

```C++
vector<int> vec;
sort(vec.begin(),vec.end());
```

给定一组数据的开头和结尾，将这段数据按默认**从小到大**的顺序排序



## C++11新特性

### lambda函数

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

#### 捕获列表

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



#### 返回值

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

#### 函数本质

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



