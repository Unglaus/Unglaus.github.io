---
title: QString
date: 2024-01-25 09:57:02
tags: Qt
category: 笔记
---

# Qt的字符串操作

## 从一段字符串中提取文件名

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

### 后缀名也不要如何做

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

