# DAY 1 Introduction

## computer introduction

how to a problem
cryptic
how to think
input output
decide how to express
why 0 and 1 ,but everything.
unary 
2 进制 why
decimal system 十进制
switches 开关 transistors 晶体管
allow --1
doing math
小数 

number -- letter
standard capital A--65 0100001
indicates 
how to distinguish
context depending
mapping : ==ASCII standard code==
bits 位 最小储存单位
1 byte = 8 bit
emojis unicode characters

---

# DAY 2 Scratch & C

==algorithm 算法==

representative
### #1
step by step
correct vs faster
decrease the size of the problem
simplify
harness
programming languages
time of solving
formalizing and thinking about
code a way to express
thinking about those corner cases -- better code

### #2
functions 函数 actions and verbs
conditionals
boolean expressions 布尔运算
cycle repeat
hash symbols: angled brackets, parentheses

### #3 week 0 
scratch graphic language
events -- programming
variables
blocks 块
==arguments 参数 or a parameter==

well designed ?
introduce a bug
risk for yourself

**leverage abstractions**
readable 
The function itself has semantic 语义
perimeter fix the input
==sub problems of big problems==
to do list

if 
cursor 光标
script 脚本 vs program?
reuse the code that you wrote

### #4 C
- comments:
	- functions
		- arguments, return values
	- conditions
	- Boolean expressions
	- loops
	- variables

*focus on details that are initially important
turn blind eyes to the other things until they become important*

correctness
design
× visual mess

`integrated development environments (IDE)`

convert it to 0 and 1 (machine code)
constructions to computer
interpret

source code --complier 编译器--machine code

---

# DAY 3 C
CLI : command line interface
syntax
\n换行符
use ";" to finish a sentence;

- `function`

`escape sequences`
\n
\r
\" real double quote

principle: the same line

C feature
==head files== 
library 库

`stdio.h`
standard io .h
`printf`

manual pages
manual.cs50.io
decades ago
**have the tendency and instinct moving forward to check the official documentation**

`string` -- text
cs50.h

模块化代码

correctness, design, style

---

# DAY 4  Arrays

### #0 Lecture 2 Arrays
**review**
syntax error & logical error
declare the type of variable
占位符：`%s,name`
 

### #1 debugging调试

what's going on 

- **method 1**: use `printf` to check
```c
#include <stdio.h>

int main (void)
{
	for (int i = 0; i <= height; i++) 
	//变量初始化；条件判断；更新操作
	{
		printf("%s #\n",i);
	}
}
```

- **==method 2==** : debugger 
- letting you slow down
###### #1 create a [^breakpoint]
[^breakpoint]: where your code will break
###### #2 `debug50 ./buggy`

garbage value == default value inside (random)
> reveal the password of someone


call stack 调用栈

step into (function) & step over 

*rubber duck: talking out the problem* 向小鸭鸭提出你的疑惑

source code to complier to machine code 
==first principle==
> `make hello`
> -  `clang hello.c`
> -  `./a.out`(use default name)

[ ] `clang hello.c` (#error)
[x] `clang hello.c -lcs50` (to link in the cs50 library)
command-line arguments 命令行参数
```c
clang hello.c -lcs50
```
[ ] 生成`a.out`
```c
clang -o hello hello.c -lcs50
```
[x] `-o hello`==直接为生成的可执行文件命名==

第一周的`make`
==compiling==
- head files 头文件相当于复制粘贴一系列函数原型
- prototype 函数原型 `int main(void)`
**编译的过程：
pre-preprocessed  source code >> assembly code 汇编代码 >> machine code**
**compiling**： preprocessing >> compiling >> assembling >> linking

CPU 中央处理器 生成的汇编代码是针对特定CPU架构的
same C code 针对不同硬件平台也会生成不同的汇编指令
复杂层级 分解为标准化步骤：让不同开发者分工处理各个环节 分别编写针对不同编译器
计算机如何通过机器码辨别字符串 图片等等不同类型

machine code back to source code ? 拆分[x]
并不是所有编程语言都需要编译

不同数据类型占用多少byte
![[Pasted image 20260815144633.png]]
string: `hi` 2 bytes; `hello`  5 bytes

a stick of memory, a dim
black chips contain lots of room for zeros and ones
1 gigabyte = 1GB = 1 billion bytes
![[Pasted image 20260815145029.png]]
***
## ==关于浮点数==

### 📊 C语言浮点数完整对照表（含内存大小与占位符）

| 精度等级      | C语言类型         | 内存大小（常见平台）              | `printf` 输出占位符 | `scanf` 输入占位符 | 字面量示例   |
| --------- | ------------- | ----------------------- | -------------- | ------------- | ------- |
| **单精度**   | `float`       | **4 字节（32 位）**          | `%f`           | `%f`          | `3.14f` |
| **双精度**   | `double`      | **8 字节（64 位）**          | `%f`           | `%lf`         | `3.14`  |
| **扩展双精度** | `long double` | **≥ 8 字节（常见 12/16 字节）** | `%Lf`          | `%Lf`         | `3.14L` |
### ⚠️ 核心规则与避坑指南（必看）

#### 1. 为什么 `printf` 里 `float` 和 `double` 都用 `%f`？

- **原因**：在 C 语言中，`float` 作为可变参数（比如传给 `printf`）时，会被**自动提升为 `double`**。所以 `printf` 根本没见过原始的 `float`，它看到的永远是 `double`。因此，**一个 `%f` 通吃 `float` 和 `double`**。

#### 2. 为什么 `scanf` 里必须严格区分 `%f` 和 `%lf`？

- **原因**：`scanf` ==接收的是**指针**（变量的内存地址）==，不是直接传值。它必须确切知道要写入的内存大小（`float` 占 4 字节，`double` 占 8 字节）。
- **如果写错**：比如用 `%f` 读取给 `double` 变量，`scanf` 只会修改前 4 个字节，导致数据错乱，产生**垃圾值**。

```c
float f;
double d;
scanf("%f", &f);   // ✅ 正确，读取单精度
scanf("%lf", &d);  // ✅ 正确，读取双精度
scanf("%f", &d);   // ❌ 严重错误！内存溢出/数据损坏
```

### ⚠️ 关于 `long double` 内存大小的特别说明

C语言标准只规定 `long double` **不低于** `double` 的精度，但没有固定具体字节数，因此**不同编译器/平台差异极大**：

| 平台 / 编译器                        | `sizeof(long double)` 常见值  | 实际精度                     |
| ------------------------------- | -------------------------- | ------------------------ |
| **Windows (MSVC)**              | 8 字节                       | 等同于 `double`（64 位），无实际提升 |
| **Linux / macOS (GCC / Clang)** | 16 字节（内部使用 80 位，填充至 16 字节） | 约 18~19 位有效十进制数          |
| **部分嵌入式平台**                     | 8 字节 或 12 字节               | 视硬件支持而定                  |
***
***
### #3 arrays 数组
An array is a chunk of contiguous memory back to back to back
~~内存块~~
`int scores[3]`: 存储三个整数

**method 1**
```c
#include <stdio.h>

int main(void)
{
	int score1 = 72;
	int score2 = 73;
	int score3 = 33;
	
	int average = (score1 + score2 + score3) / 3;

	printf("Average: %i\n", average);
}
```

**method 2**
```c
#include <stdio.h>

int main(void)
{
	int scores[3];
	scores[0] = 72;
	scores[1] = 73;
	scores[2] = 33;
	
	printf("Average: %f\n", (score[0] + score[1] + score[2]) / 3.0);
}
```
在数组中连续储存

**method 3**
```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int scores[3];
    for (int i = 0; i < 3; i++)
    {
        scores[i] = get_int("Score:");
    }
    printf("Average: %f\n", (scores[0] + scores[1] + scores[2]) / 3.0);
}
```
[ ] 3被硬编码了
```c
const int N = 3
//CONSTANT 常量使用大写
```

### ==the final version==

```c
// Averages three numbers using an array, a constant, and a helper function

#include <cs50.h>
#include <stdio.h>

// Constant
const int N = 3;

// Prototype
float average(int length, int array[]);

int main(void)
{
    // Get scores
    // #1 通过循环从用户处得到数据
    int scores[N];
    for (int i = 0; i < N; i++)
    {
        scores[i] = get_int("Score: ");
    }

// Print average
// #2 取平均并打印
//（此处为简化写法，将声明函数写在开头，具体用法写在最末）
    printf("Average: %f\n", average(N, scores));
}

//#2 用于定义取平均，利用int length定义数组长度（去多少个数），利用int array[]简化变量编号过程

float average(int length, int array[])
{
    // Calculate average
    int sum = 0;
    for (int i = 0; i < length; i++)
    {
        sum += array[i];
    }
    return sum / (float) length;
}
```

---
