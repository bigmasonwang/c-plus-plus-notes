## 一个简单的c++程序

首先来看一个简单的c++程序:

```c++
#include <cstdlib>
#include <iostream>
int main() {
	int x, y;
	std::cout << "Please enter two numbers: ";
	std::cin >> x >> y;
	int sum = x + y;
	std::cout << "Their sum is " << sum << std::endl;
	return EXIT_SUCCESS;
}
```

我们知道c可以用gcc编译. 与此相似, 上述c++代码可以通过g++编译, 生成名为`a.out`的可执行文件. 

最开始的两行称为头文件(*header files*). `cstdlib`为一个标准库, 传承自c语言的库`stdlib.h`, 内含常用函数, 包括`abs()` `rand()` `sort()`等; `iostream`为一个IO流库, 注意用流进行输入输出的效率有点低, 而使用c标准库`stdio` 的 `printf/scanf` 效率会较高.

接下来, 我们发现`main()`函数有`int`类型的返回值, 视线转向最后, 程序return了`EXIT_SUCCESS`这样的一个变量, 这个变量的值若为0则表示程序执行成功; 相应的, 如果程序执行失败会返回一个非0的值. 当然这一语句可以直接写成 `return 0;`.

随后, 程序的输入输出语句`cout/cin`并不像常见的`printf/scanf`, `<<`是输出符, `>>`为输入符. 语句一开始的`std::`为标准库中的objects, 类似于java中的`System.out`.



## 基本数据类型

### Characters

一般来说, 在c++中一个`char`为8-bits, 即一个byte. `char`类型的字符由单引号括起来. 除了单个数字和字母以外, 还有一些转义字符:

| 字符 | 含义      |
| ---- | --------- |
| '\n' | newline   |
| '\b' | backspace |
| '\0' | null      |
| '\t' | tab       |
| '\r' | return    |

### Integers 

整数变量有三种: `short` `int` `long`. 

这三者的大小在不同的系统中有可能不同, 可以通过`sizeof()`函数可得知当前机器中变量的大小.

### Float Point

浮点数变量有两个: `float`单精度浮点数与`double`双精度浮点数.

那么这个精度指的是什么? 经过查询[资料](https://www.zhihu.com/question/26022206), 如下:

单精度浮点数为32-bit, 其中1-bit符号, 8-bit指数, 23-bit小数.

### ![float](../images/float.png)

单精度时指数偏移度为127，目的是为了同时可以表示正和负的指数，即00000000-11111111分别对应-127 -- 128. 图一中指数应该为124-127=-3. 而小数部分为0.01，即这个数为1.01*2^-3 =0.00101（2进制)。换成10进制为0.125+0.03125=0.15625

而双精度浮点数为64-bit, 其中1-bit符号, 11-bit指数, 52-bit小数.

![double](../images/double.png)

### 测试

因为c++追求高效(efficiency), 各种数据类型在不同环境中编译后所占空间大小会不尽相同, 折让程序员头皮发麻.

为了测试在本机中数据类型的大小, 在[runoob](https://www.runoob.com/cplusplus/cpp-data-types.html)找到一份代码

```c++
#include<iostream>
#include<string>
#include <limits>
using namespace std;

int main()
{
    /*
    signed, unsigned, long和short都隐含了int, 等价于signed int, unsigned int, long int, short int
    但注意char没有这种默认等价性。char不和signed char或者unsigned char其中任何一个等价。使用char的时候最好标明是signed char还是unsigned char。
    signed与signed int与int是等价类型
    */
    cout << "type: \t\t" << "************size**************" << endl;
    // *
    cout << "--------------------------------" << endl;
    int *p;
    cout << "*p: \t\t" << "所占字节数：" << sizeof(p) << endl;

    // bool
    cout << "--------------------------------" << endl;
    cout << "bool: \t\t" << "所占字节数：" << sizeof(bool);
    cout << "\t最大值：" << (numeric_limits<bool>::max)();
    cout << "\t\t最小值：" << (numeric_limits<bool>::min)() << endl;

    // char
    cout << "--------------------------------" << endl;
    cout << "char: \t\t" << "所占字节数：" << sizeof(char);
    cout << "\t最大值：" << (numeric_limits<char>::max)();
    cout << "\t\t最小值：" << (numeric_limits<char>::min)() << endl;

    cout << "signed char: \t" << "所占字节数：" << sizeof(signed char);
    cout << "\t最大值：" << (numeric_limits<signed char>::max)();
    cout << "\t\t最小值：" << (numeric_limits<signed char>::min)() << endl;

    cout << "unsigned char: \t" << "所占字节数：" << sizeof(unsigned char);
    cout << "\t最大值：" << (numeric_limits<unsigned char>::max)();
    cout << "\t\t最小值：" << (numeric_limits<unsigned char>::min)() << endl;

    // short (typedef short int wchar_t;)
    cout << "--------------------------------" << endl;
    cout << "short: \t\t" << "所占字节数：" << sizeof(short);
    cout << "\t最大值：" << (numeric_limits<short>::max)();
    cout << "\t\t最小值：" << (numeric_limits<short>::min)() << endl;

    cout << "unsigned short:\t" << "所占字节数：" << sizeof(unsigned short);
    cout << "\t最大值：" << (numeric_limits<unsigned short>::max)();
    cout << "\t\t最小值：" << (numeric_limits<unsigned short>::min)() << endl;

    cout << "wchar_t: \t" << "所占字节数：" << sizeof(wchar_t);
    cout << "\t最大值：" << (numeric_limits<wchar_t>::max)();
    cout << "\t\t最小值：" << (numeric_limits<wchar_t>::min)() << endl;

    // int
    cout << "--------------------------------" << endl;
    cout << "int: \t\t" << "所占字节数：" << sizeof(int);
    cout << "\t最大值：" << (numeric_limits<int>::max)();
    cout << "\t最小值：" << (numeric_limits<int>::min)() << endl;

    cout << "unsigned: \t" << "所占字节数：" << sizeof(unsigned);
    cout << "\t最大值：" << (numeric_limits<unsigned>::max)();
    cout << "\t最小值：" << (numeric_limits<unsigned>::min)() << endl;

    // long
    cout << "--------------------------------" << endl;
    cout << "long: \t\t" << "所占字节数：" << sizeof(long);
    cout << "\t最大值：" << (numeric_limits<long>::max)();
    cout << "\t最小值：" << (numeric_limits<long>::min)() << endl;

    cout << "unsigned long: \t" << "所占字节数：" << sizeof(unsigned long);
    cout << "\t最大值：" << (numeric_limits<unsigned long>::max)();
    cout << "\t最小值：" << (numeric_limits<unsigned long>::min)() << endl;

    // double
    cout << "--------------------------------" << endl;
    cout << "double: \t" << "所占字节数：" << sizeof(double);
    cout << "\t最大值：" << (numeric_limits<double>::max)();
    cout << "\t最小值：" << (numeric_limits<double>::min)() << endl;

    cout << "long double: \t" << "所占字节数：" << sizeof(long double);
    cout << "\t最大值：" << (numeric_limits<long double>::max)();
    cout << "\t最小值：" << (numeric_limits<long double>::min)() << endl;

    // float
    cout << "--------------------------------" << endl;
    cout << "float: \t\t" << "所占字节数：" << sizeof(float);
    cout << "\t最大值：" << (numeric_limits<float>::max)();
    cout << "\t最小值：" << (numeric_limits<float>::min)() << endl;

    cout << "size_t: \t" << "所占字节数：" << sizeof(size_t);
    cout << "\t最大值：" << (numeric_limits<size_t>::max)();
    cout << "\t最小值：" << (numeric_limits<size_t>::min)() << endl;

    cout << "string: \t" << "所占字节数：" << sizeof(string) << endl;
    // << "\t最大值：" << (numeric_limits<string>::max)() << "\t最小值：" << (numeric_limits<string>::min)() << endl;

    cout << "type: \t\t" << "************size**************" << endl;

    return 0;
}
```

编译运行后发现:

```
type: 		************size**************
--------------------------------
*p: 		所占字节数：8
--------------------------------
bool: 		所占字节数：1	最大值：1		最小值：0
--------------------------------
char: 		所占字节数：1	最大值：		最小值：�
signed char: 	所占字节数：1	最大值：		最小值：�
unsigned char: 	所占字节数：1	最大值：�		最小值：
--------------------------------
short: 		所占字节数：2	最大值：32767		最小值：-32768
unsigned short:	所占字节数：2	最大值：65535		最小值：0
wchar_t: 	所占字节数：4	最大值：2147483647		最小值：-2147483648
--------------------------------
int: 		所占字节数：4	最大值：2147483647	最小值：-2147483648
unsigned: 	所占字节数：4	最大值：4294967295	最小值：0
--------------------------------
long: 		所占字节数：8	最大值：9223372036854775807	最小值：-9223372036854775808
unsigned long: 	所占字节数：8	最大值：18446744073709551615	最小值：0
--------------------------------
double: 	所占字节数：8	最大值：1.79769e+308	最小值：2.22507e-308
long double: 	所占字节数：16	最大值：1.18973e+4932	最小值：3.3621e-4932
--------------------------------
float: 		所占字节数：4	最大值：3.40282e+38	最小值：1.17549e-38
size_t: 	所占字节数：8	最大值：18446744073709551615	最小值：0
string: 	所占字节数：24
type: 		************size**************
```



