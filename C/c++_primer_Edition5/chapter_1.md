# 1.1 初识输入输出

C++未定义任何输入输出语句(IO)，使用标准库(standard library)-(`#include <iostream>`)提供IO机制。`iostream`库包含两个基础类型`istream`和`ostream`，分别表示输入流和输出流。一个流是一个字符序列。

## 1.1.1 标准输入输出对象

标准库定义了4个IO对象。

```c++
/*
** cin: 标准输入(standard input),istream对象
** cout: 标准输出(standard output),ostream对象
** cerr: 输出警告和错误消息，ostream对象
** clog: 输出程序运行时的一般性信息;ostream对象
*/
```

## 1.1.2 读取数量不定的输入数据

```c++
// 描述： 输入一组数求和，输入个数不定
#include <iostream>
int main()
{
    int sum = 0, value = 0;
    // 读取数据直到文件尾，计算所有读入的数的和
    while (std::cin >> value)
    {
        sum += value;
    }
    std::cout << "Sum is: " << sum << std::endl;
    return 0;
}
```

代码解析：

while的循环条件是对表达式`std::cin >> value`求值；输入运算符`>>`返回其左侧运算对象，在本例中是`std::cin`，所以循环条件检测的是`std::cin`。

以`iostream`对象作为条件时，其实就是检测流的状态。如果流是有效的，即流未遇到错误，那么检测成功；当遇到文件结束符(end-of-file)-(在windows上面是`Ctrl+Z` 在Linux/Unix上面是`Ctrl+D`)，或者遇到一个无效输入时，`istream`对象的状态变为无效，条件为假。