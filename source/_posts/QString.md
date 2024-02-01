---
title: QString
date: 2024-01-25 09:57:02
tags: Qt
category: 笔记
---

# Qt的字符串操作--QString

## 从一段字符串中提取文件名--QFileInfo.fileName()

读取文件名时通常得到的是带有文件路径的一串字符串，有时候只想要最后的那个文件名，这时就可以使用`QFileInfo`类的`fileName()`函数来实现

```cpp
#include <iostream>
#include <QString>
int main() {
    QString filePath = "/path/to/file.txt";
    
    // 使用QString的方法提取文件名
    QString filename = QFileInfo(filePath).fileName();
    
    std::cout << "Filename: " << filename.toStdString() << std::endl;
    
    return 0;
}
```

```bash
Filename: file.txt
```

## 后缀名也不要如何做--QFileInfo.baseName()

这时要使用`QFileInfo`类的`baseName()`函数

```cpp
#include <iostream>
#include <QString>

int main() {
    QString filePath = "/path/to/file.txt";
    
    // 使用 QFileInfo 的 baseName() 函数去掉文件后缀名
    QString filename = QFileInfo(filePath).baseName();
    
    std::cout << "Filename without extension: " << filename.toStdString() << std::endl;
    
    return 0;
}
```

```bash
Filename withour extension: file
```

***

**实现原理：**`QFileInfo` 类的 `baseName()` 函数是通过查找文件名中最后一个点（.）之后的部分来确定文件的后缀。它将点之后的部分视为文件的后缀，并返回文件名中点之前的部分作为基本名称。

***

注意上面提到了，是通过查找文件名中**最后一个**点（.）之后的部分来确定文件的后缀。所以如果对字符串`aaa.bbb.ccc`使用`baseName()`，首先会得到`aaa.bbb`，对这个字符串再使用一次`baseName()`，会得到`aaa`

## 匹配字符串末尾--QString.endsWith()

使用 `QString` 的 `endsWith()` 函数来实现

```cpp
#include <QString>
#include <iostream>

int main() {
  QString str = "Hello, world!";

  // 使用endsWith函数检查后缀
  if (str.endsWith("world!")) {
    std::cout << "String ends with 'world!'" << std::endl;
  } else {
    std::cout << "String does not end with 'world!'" << std::endl;
  }

  return 0;
}
```

在上述示例中，我们创建了一个 `QString` 对象 `str`，并使用 `endsWith` 函数来检查字符串是否以指定的后缀 `"world!"` 结尾。如果字符串以指定的后缀结尾，我们输出 "String ends with 'world!'"，否则输出 "String does not end with 'world!'"。

通过使用 `endsWith()` 函数，你可以检查 `QString` 对象是否以指定的后缀结尾，并根据需要执行相应的操作。

***

相比`QFileInfo.baseName()`，`QString.endsWith()`不需要用（.）来分隔字符串，以确定后缀的内容，它就是根据你给定的字符串，去对一段字符串最后的几个字符进行字符匹配，若匹配上则返回`true`，否则返回`false`

## QString和string的相互转换

### `QString`转`std::string`

使用`QString::toStdString()`函数

```cpp
#include <iostream>
#include <string>
#include <QString>

int main() {
    QString qstr = "Hello, world!";    
    std::string str = QString::toStdString(qstr);    
    std::cout << "string: " << str <<std::endl;
    return 0;
}
```



### `std::string`转`QString`

使用`QString::fromStdString()`函数

```cpp
#include <iostream>
#include <string>
#include <QString>

int main() {
    std::string str = "Hello, world!";   
    QString qstr = QString::fromStdString(str);    
    std::cout << "Converted QString: " << qstr.toStdString() << std::endl;
    return 0;
}
```

这里`cout`输出的时候可以看到其实又用`toStdString`转成`string`来输出了，毕竟`std::cout`支持的输出类型中有`std::string`而没有`QString`

