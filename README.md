# C++学习笔记（C++11）

## 处理数据

### 整型

C++提供多种整型，能够根据程序的具体要求选择最合适的整型

- 符号类型（正负值的取值范围几乎相同）：short、int、long、long long

- 在C++中，**并没有规定每一类整型要占多少空间，只是规定了至少要占多少空间**

  **sizeof**表示多少字节，1字节等于8位，那么64位则是8字节

  - short：**至少占16位**

  - int：至少与short一样长

  - long：**至少32位**，且不短于int

  - long long：**至少64位**，且不短于long

  ```c++
  short score;
  int temperature;
  long position;
  long long lang_lang;
  ```

  

- 无符号类型（无负数）

  使用unsigned关键字

  ```c++
  unsigned short change;
  unsigned int rovert;
  unsigned long gone;
  unsigned long long lang_lang;
  ```

  

- 变量初始化

  **如果不对变量赋予初始值，则不要引用这个变量，因为该变量的值将是不确定的**

  

- 不同进制的整型表示

  ```c++
  int chest = 42; //十进制
  int waist = 0x42; //十六进制
  int inseam = 042; //八进制（以0开头的）
  ```

  不管是以什么进制表示，在内部都会转换为二进制，如果使用cout来输出，那么默认是都输出十进制的表示

  

- 确定整型常量的类型

  **用后缀明确指出常量类型**

  **十进制默认都是int**，**八进制和十进制常量默认是合适范围的无符号数**

  - L或I：长整型。如100L
  - U或u：无符号数。如100U
  - LU或UL：无符号长整型
  - LL或ll：long long类型
  - LLU或uLL：无符号long long类型

### char类型

处理字符的类型

**8位**

常用编码：ASCII

- char类型的运算

  可以执行加减运算或比较运算，参加运算的是内码值

  ```c++
  char ch = 'M';
  
  // #1
  ch = ch + 1;
  // 输出ch，大写字母是连续编码
  ch = N
      
  // #2
  ch = ch - 1;
  // 输出ch，大写字母是连续编码
  ch = L
  ```

  

- char类型赋初值用**单引号**

  ```c++
  char ch = 'A'; //键盘上存在的字符
  char ch_n = '\n'; //转义字符
  ```



### bool类型

用一个字节表示（1个字节等于8位二进制）

**8位**

**true是1，false是0**

可以作为算术运算的运算数



### 符号常量的定义

const限定符：限定一个变量是**只读**的

必须给初值

```c++
const double PI = 3.1416;
```

符号常量命名一般全部大写



### 浮点数

实型

- 二进制浮点数的机内形式
  $$
  10100 * 2^{1101}
  $$

​	分别保存10100和1101，前者称为尾数，后者称为指数

- 浮点类型
  - float：至少32位
  - double：至少48位，且不少于float
  - long double：至少和double一样

​	浮点常量默认是**double**类型

​	**浮点数不能精确表示（近似值）**

​	float类型7位精度，double类型15位精度，例如

​	

```c++
float a = 1.800000;
double b = 1111111.111111;
```



- 科学计数法

  E或者e表示10的多少次方，例如
  $$
  -1.5E10 = -1.5*10^{10}
  $$

  $$
  34e-8 = 34 * 10^{-8}
  $$

  常用来表示非常大或非常小的实数

  

- 明确指出浮点常量的类型

  - float：F或f
  - long double：L或l

  例如：1.5f，2.3E10L

  

### 运算表达式

加、减、乘、除、取模（%）

取模结果是**两个整数相除的余数**

- 除法的结果

  除法的结果取决于运算数

  **两个整数相除的结果是整数**

  例如 5 / 2 = 2，而不是2.5，因为两个都是整数

  **只要有一个运算数是浮点数，则会保留小数部分**

  例如 5.0 / 2 = 2.500000

  **只要有一个运算数是double，那么结果是double**

  **如果都是float，结果是float**

  

- 类型转换

  - **自动转换类型**，例如

  ```c++
  float a = 3;
  //输出
  a = 3.000000
  
  int ii = 3.9832;
  //输出，直接把小数点扔掉（即向下取整，而不是四舍五入）
  ii = 3
  ```

  转换规则

  希望**计算结果尽可能准确**，因此，转换原则是**精度小的类型向精度大的类型转换**，例如float转double

  

  - **强制类型转换**

    ```c++
    //类型（表达式）
    int x = 5, y = 2;
    cout << (double)x/y; //C风格的类型转换：(类型)表达式
    //结果为2.5
    
    cout << 'A' << '\t' << int('A'); //C++风格的类型转换：类型(表达式)
    //结果为 A 65(A的内码值(ASCII))
    ```

## 复合类型

### 数组

- 定义格式

​	类型 数组名[元素个数];

​	类型 数组名[元素个数] = {初值表};

​	例如

```c++
int array[10]; //如果不赋值，那么每个元素的初始值为随机值（可能是内存之前存储的数据的残留）
int zarray[10] = {0}; //每个元素初始值为0
int znarray[10] = {}; //每个元素初始值为0
double darray[3] = {1.1, 2.1, 3.4};
short sarray[10] = {0, 1, 1};// 前三个元素值为0，1，1，其余的元素的初始值为0
int nnarray[] = {0, 1, 2}; //让编译器根据初值数量来决定数组大小
```

 

- 数组元素的表示

  数组名[下标]

  **注意：编译器不会检查下标的合法性！！！一定不要超出范围**



### C风格的字符串

**双引号**包围 "programming"

以`'\0'`结束的一串字符，`'\0'`为空字符，以字符数组的形式存储

```c++
char str[] = {'s', 't', 'r', 'i', 'n', 'g', '\0'}; 		//占7个字节
char str[] = "string"; 									//占7个字节
char str[10] = "string"; 								//占10个字节
//第三个数组的全部元素为
{'s', 't', 'r', 'i', 'n', 'g', '\0', '\0', '\0', '\0'}
```

**注意：字符数组和字符串的区别**

```c++
char str[] = {'s', 't', 'r', 'i', 'n', 'g', '\0'}; 		//这个是字符串
char str[] = {'s', 't', 'r', 'i', 'n', 'g'}; 			//这个是字符数组
```

**字符串必须以`'\0'`结束**

**空字符串""占用一个字节的空间，存放空白字符，即`'\0'`**



### C++风格的字符串

string类

头文件名string，在命名空间std中

```c++
#include <string>
using namespace std;
```

- 变量定义

  ```c++
  string str1, str3;
  string str2 = "hello";
  ```

- 字符串复制、拼接

  ```c++
  str1 = str2;
  str3 = "abced";
  str2 += str3;
  str3 = str1 + str2;
  ```

### 结构简介

- struct关键字

```c++
struct book {
    char title[MAXTITL];
    char author[MAXAUTL];
    float value;
};
```

- 定义结构变量、数组

```c++
book book1, bookarray[10];
```

- 结构变量赋初值

```c++
book book1 = {"C", "abc", 89.0};
book bookarray[2] = {{"C", "abc", 89.0}, {"C++", "abc", 99.0}};
```

- 结构变量赋值

​	同类变量直接赋值

```c++
bookarray[0] = bookarray[1];
```

- 成员

  ```c++
  book1.author
  bookarray[2].title
  ```

### 指针简介

**指针：值为内存地址的变量**

用途：提供间接访问

定义指针变量：类型名 *指针变量名

```c++
int *p;
```

**运算符&**：一元运算符，运算对象是变量，运算结果是变量的地址

```c++
int *p, a;
p = &a; //将变量a的内存地址存放在指针变量p中
```

**间接访问运算符***：一元运算符，运算对象是指针，运算结果是指针指向的变量

```c++
*p = *p * 2 //将p指向的变量值乘2后赋值回去
```

**注意**

- **不要使用没有初始化的指针**

  ```c++
  int *p;
  *p = 223 //指针变量没有存储内存地址，访问的内存地址将是不可预知的
  ```

- **不要直接给指针赋一个整数**

  ```c++
  double *p;
  p = 65536; //指针变量存储的是内存地址，而直接赋一个整数将会访问意料之外的内存地址（十六进制）
  ```

- **不同类型的指针之间不能赋值**

  ```c++
  int a, *intp = &a;
  double *doublep;
  doublep = intp; //指针变量的类型会告诉c++，在这个内存地址上读几个字节的数据，并解释为该类型；而不同类型的指针会造成解释错误（例如本来读4字节，结果读8字节，剩下的4个字节是别的数据，那么数据就不对了）
  ```



### 动态内存分配

程序通过声明变量通知计算机为它准备好内存空间，这些信息是编译时就能确定的

每个变量对应一块内存空间

变量名是这块空间的名字，程序通过变量名访问对应的空间



动态内存分配：**在程序运行时申请内存和释放内存的功能**



#### **动态内存申请**

在内存中寻找一块大小合适的空间，返回起始地址

动态分配的内存没有名字，只有地址，只能**通过指针间接访问**



**动态内存申请方法**

new 类型							       申请一块保存某种类型 **数据** 的内存空间，返回申请到的内存地址

new 类型[结果值为整数的表达式]		      申请一块保存某种类型 **数组** 的内存空间，返回申请到的内存地址

```c++
int *intp = new int; 				//申请存储一个整型数的动态内存
int *array = new int[20]; 			//申请一个20元素的整型数组
int *array = new int[n]; 			//申请一个n个元素的整型数组
```



#### **内存释放**

通过变量声明获得的内存会在存储期结束时收回

**动态申请的空间不会被系统主动收回**

没有delete的动态内存一直被占用

特别是程序执行结束，这块空间还被标识为使用，还不能释放，这就是**内存泄漏**



**释放空间的运算**

delete 指针

**如果指针指向数组**

delete [] 指针

**不管什么类型的指针占用空间都是4个字节**（32位系统）



### 指针运算

允许四种运算：++、--、+、-

指针变量+1，等于增加它**指向的类型的字节数**，例如指向double的指针+1后，则指针数值增加8（字节），即指针往后移动了8个字节

这个运算会在不影响内存位置中实际值的情况下，**移动指针到下一个内存位置**



**c++将数组名解释为数组第一个元素的地址（数组的起始地址）**

即**数组名是一个指针**，例如，一个double数组的数组名就是一个指向double类型的指针 



通过指针，顺序访问数组中的每一个元素

```c++
int arr[5] = {8, 16, 32, 64, 128};
int *ptr;

ptr = arr; //将数组第一个元素的地址赋值给指针

for (int i = 0; i<5; i++)
{
    std::cout << "address of arr[" << i << "] = ";
    std::cout << ptr << std::endl;

    std::cout << "Value of arr[" << i << "] = ";
    std::cout << *ptr << std::endl;
    
    // 移动到下一个位置
    ptr++;
}
```

输出结果

```
address of arr[0] = 0x7ffee2edb1e0
Value of arr[0] = 8
address of arr[1] = 0x7ffee2edb1e4
Value of arr[1] = 16
address of arr[2] = 0x7ffee2edb1e8
Value of arr[2] = 32
address of arr[3] = 0x7ffee2edb1ec
Value of arr[3] = 64
address of arr[4] = 0x7ffee2edb1f0
Value of arr[4] = 128
```



### 指针与字符串

C风格的字符串（字符数组形式存储）可以用指针来表示

```c++
char str[] = "string"; 			//这是数组的写法
const char *str = "string"; 	//只读的C风格字符串，这是用了指针的写法，相当于str这个指针存储 char str[] = "string" 这个字符数组的内存地址
```



### 动态结构

运行时通过new申请一个动态的结构变量

#### 申请动态结构

结构指针 = new 结构类型;

```c++
struct inflatable
{
    char name[20];
    float volume;
    double price;
};
inflatable *ptr;
ptr = new inflatable;

//释放
delete ptr;
```

#### 访问动态结构

(*指针).成员

必须用括号括起来（因为.的运算优先级比*要高，所以一定要加括号）



上面的太麻烦，因此用下面的简洁



指针->成员

例如 ptr->name



### 数组的替代品

#### 类模板vector

**动态数组，可以自动调整长度**

需要包含头文件vector

定义时，需要指出数据类型和规模

**规模可以是变量**

```c++
vector<int> v1;			//规模为0
int n;
cin >> n;
vector<double> v2(n);	//规模用圆括号
```



#### array

效率比vector高的数组，规模固定（因为规模固定所以效率比vector高）

C++11新增类型

需要包含头文件array

定义时，需要指出数据类型和规模

**规模是常量**

```c++
array<int, 5> a1;
array<double, 4> a2 = {1.0, 2.3, 2.1, 4.2};
```



#### 与普通数组的区别

array可以直接通过等号，将a3的内容拷贝到a4上，而普通数组不可以，因为普通数组只能对数组下标的元素进行操作赋值，而不能对数组名赋值操作，因为数组名是指针，指向的是内存地址。

```c++
array<double, 4> a3 = {1.0, 2.3, 2.1, 4.2};
array<double, 4> a4;
a4 = a3;
```

- 可以像数组一样通过下标变量访问
- 可以整体直接赋值（内容拷贝，内存地址是不同的）



## 循环和关系表达式

### for循环



#### 常规格式

**for (表达式1;表达式2;表达式3)**

1. 先执行表达式1
2. 表达式2，真继续循环，假结束循环
3. 执行循环体
4. 执行表达式3



例如：

for (计数器赋初值; 检查是否达到指定次数; 修正计数器值)

```c++
for (i = 1; i<= 10; i=i+1)
{
    cout << i << '\t';
}
```



**使用逗号表达式**

**在只允许出现一个表达式的地方放多个表达式**，用逗号分隔

```c++
string word;
cin >> word;

char temp;
int i, j;

for (j = 0, i = word.size() - 1; j < i; --i, ++j)
{
    temp = word[i];
    word[i] = word[j];
    word[j] = temp;
}
```



#### 范围for循环

C++11的扩展

for (循环变量：数组或列表)

```c++
//这是单个语句的写法，加了花括号即为复合语句，单个语句可以不加花括号
for (int x: {1, 2, 3})
    cout << x << '\t';

double darray[4] = {1.2, 2.1, 3.2, 2.3};
for (double x: darray)
{
    cout << x << '\t';
}
```



#### 递增递减运算符

| ++             | --             |
| -------------- | -------------- |
| 一元运算符     | 一元运算符     |
| 将运算对象加一 | 将运算对象减一 |



**不论是前缀还是后缀，++k或是k++，对于k都是改变的，即k+1;**

**但是如果将++k或是k++放在一个大的表达式里，例如 y=++k，那么y所获得的值是不一样的**



前缀：

运算对象本身，即将运算后的值作为结果，即k+1

++k，--k



后缀：

修改前的运算对象值，即将原始k作为结果

k++，k--



例如

```c++
x = 5;

y = ++x;  //此时x=6,y=6

y = x++;  //此时x=6,y=5
```

**简单来说，前缀先算，后缀后算**

比如前缀，那么结果就是运算后的；如果x在前面，结果就是一开始的x



### while循环

用在循环次数不确定的情况

```c++
while (测试条件)
```

1. 先执行测试条件，测试条件为真时，继续循环，为假就结束循环
2. 再执行循环体



**是没有初始化和更新部分的for循环**



### do...while循环

用在循环次数不确定的情况

执行顺序跟while相反，先执行一遍循环体，再判断是否继续循环，因此无论如何，do...while循环都会至少执行一遍循环体

```c++
do
	循环体
while (测试条件)
```

1. 先执行循环体
2. 再执行测试条件，测试条件为真时，继续循环，为假就结束循环



### 二维数组与嵌套循环

二维数组

类型名 数组名[常量1] [常量2]

```c++
int a[3][4];

//二维数组的初始化
int a[3][4] = {{1,2,3,4}, {5,6,7,8}, {9,10,11,12}};
```

嵌套循环

外层处理行，里层处理列

```c++
for (int i = 0;i < 10;++i)
{
    cout << array[i] << '\t';
    for (int j = 0;j < 9;++j)
        cout << array[i][j] << '\t';
}
```



## 分支语句和逻辑运算符

### if语句



### 逻辑表达式

与 **&&**：两个都为真，即为真，否则为假

或 **||**：有一个为真，即为真

非  **!** :   反转



### 条件表达式

**用于取代简单的if语句**

表达式1  ?  表达式2  :  表达式3

如果表达式1为真，则输出表达式2的结果，否则用表达式3的结果

```c++
if (a > b)
    max = a;
else
    max = b;

//简化为
max = a > b ? a:b;
```



### switch语句

实现多分支的语句

```c++
switch (表达式)
{
    case 常量1:
        语句1
    case 常量2:
        语句2
    default:
        语句3
}
```



**break**

跳出循环

**continue**

跳出当前循环



## 函数

### 数组传递

```c++
int sum_arr(int arr[], int n);
```

将数组以指针形式传递

```c++
int sum_arr(int *arr, int n);
```



如果是传递数组，**为了可读性**，最好是使用数组的形式来表示，不然很容易误以为是别的指针

```c++
int sum_arr(int arr[], int n);
```



### 函数指针

将函数指针作为函数参数 ，例如回调函数

定义

返回类型 (*指针变量名)(形式参数表);

```c++
//指针要指向的函数
int isdigit(int n, int k);

//定义函数指针，注意圆括号一定要加
int (*p)(int, int);

//指向这个函数（将目标函数名赋值给函数指针）
p = isdigit;

//直接通过函数指针调用目标函数
a = p(n, k);
```

例如

```c++

// 定义一个函数类型
typedef void (*PrintFunction)(int);

void printHello(int x) {
    std::cout << "Hello: " << x << std::endl;
}

void printWorld(int x) {
    std::cout << "World: " << x << std::endl;
}

int main() {
    PrintFunction myFunc = printHello;
    myFunc(10); // 输出 "Hello: 10"

    myFunc = printWorld;
    myFunc(20); // 输出 "World: 20"

    return 0;
}
```



### 内联函数

有函数的形式，但无函数调用的代价

编译时用函数体替换函数调用，没有函数调用的代价



使用**inline**关键字



**函数定义必须再函数调用之前**

```c++
inline double square(double x){return x * x;}		//内联函数

int main()
{
    a = square(5.0);		//在程序执行的时候，实际上这行的代码是 a = 5.0 * 5.0; 编译器会自动替换掉，而不是去调用函数
    
    return 0;
}
```



### 引用变量

变量的别名

c++不会分配新的内存空间



引用变量的声明

类型 &变量名 = 已有的同类变量;

```c++
int k;
int &j = k;
```

用途：作为函数的参数，代替指针传递，使函数可以修改实际参数（**实际参数的别名**）

```c++
void swap(int &a, int &b)
{
    int temp;
    temp = a;
    a = b;
    b = temp;
}//直接修改了a、b的值
```

引用传递的实际参数必须是一个变量，不能用表达式



提高参数传递效率



如果形式参数前加**const**修饰，那么实际参数可以是值、变量、表达式，因为此时只读



#### 引用返回

类型 &函数名 (形式参数表)

返回的是 返回变量的别名



**作用**

将函数用于赋值运算符的左边，即作为左值

减少函数返回时的开销



**注意**

返回值必须是离开函数后依然存在的左值

返回类型前可以加**const**,此时函数不能作为左值（此时仅仅是减少函数返回时的开销）



例子1

```c++
int a[] = {1,3,5, 5, 7, 9};
int &index(int);

int main()
{
    index(2) = 25;			//此时可以将函数用于赋值运算符的左边，即作为左值，这样就能够直接对a[2]赋值
	cout << index(2);
}

int &index(int j)
{
    return a[j];
}
```



例子2	链式调用

```c++
#include <iostream>
#include <string>
using namespace std;

class Person {
    public:
        string name;

        Person(const string& n) : name(n) {}	//构造函数

        Person& setName(const string& newName) {
            name = newName;
            return *this; // 返回*this引用，支持链式调用
        }
};

int main() {
    Person p("Alice");
    p.setName("Bob").setName("Charlie"); // 作为左值，链式调用，修改同一个Person对象
    std::cout << p.name << endl; // 输出 "Charlie"
    return 0;
}
```



### 函数重载

一组同名函数

```c++
int max(int a1, int a2);
int max(int a1, int a2, int a3);
int max(int a1, int a2, int a3, int a4);
int max(int a1, int a2, int a3, int a3, int a4, int a5);
```

重载函数必须有不同的函数特征标



**何时使用函数重载**

执行相同的任务，但使用不同形式的数据



### 函数模板

c++泛型编程



实现通用函数




用参数表示函数中的变量类型

调用时，用具体的类型代入，形成一个真正的函数

```c++

template <typename T>		//也可以用 template <class T> 表示
void swap(T &a, T &b)
{
    T temp = a;
    a = b;
    b = temp;
}
```



多个模板参数

```c++
template <typename T1, typename T2>
void mix(T1 a, T2 b)
{
    //函数体
}
```



#### 显式实例化

使用函数模板时，明确指出模板参数的类型



调用方式

函数名<模板实际参数表>(函数的实际参数表)

```c++
template <class T1, class T2, class T3>
T3 calc(T1 x, T2 y)
{
    return x+y;
}

//调用
calc<int, char, char>(5, 'a');	//结果是'f'，返回是char类型
calc<int, char, int>(5, 'a');	//结果是102，返回时int类型
```



#### 让编译器自动推断返回类型

auto 函数名(形式参数表) -> decltype(表达式)

```c++
template <class T1, class T2>
auto calc(T1 x, T2 y) -> decltype(x+y)
{
    return x+y;
}

//调用
calc(5, 'a');	//结果是102，自动推断是int类型（因为int和char相加，char会自动强制转换为int类型）
```



#### 函数模板的重载

一组同名的函数模板

重载函数模板必须有不同的函数特征标

```c++
template <typename T> void Swap(T &a, T &b);
template <typename T> void Swap(T *a, T *b, int n);		//为了可读性，数组传递最好写成void Swap(T a[], T b[], int n)

template <typename T>
void Swap(T &a, T &b)
{
    //函数体
}

template <typename T>
void void Swap(T a[], T b[], int n)
{
    //函数体
}
```



#### 显式具体化

为特定类型提供一个特化版本，特殊处理

```c++
#include <iostream>
#include <string>

// 通用的函数模板
template<typename T>
void print(const T& value) {
    std::cout << "Generic print: " << value << std::endl;
}

// 显式具体化针对std::string类型的print函数
template<>
void print(const std::string& value) {
    std::cout << "Specialized print for string: \"" << value << "\"" << std::endl;
}

int main() {
    int i = 42;
    std::string s = "Hello, World!";

    print(i);   // 调用通用的print模板
    print(s);   // 调用显式具体化的print模板

    return 0;
}
```



## 内存模型和名称空间

### 名称空间

防止名字冲突

```c++
namespace A{
    int a;
    double b;
}

namespace B{
    int a;
    double b;
}
```

不同名称空间里面的名字可以相同

```c++
A::a = 9;
B::a = 2;
```



- **using声明**

将该成员加入到当前作用域，在此作用域中引用该成员不需要加名字间名的限定

```c++
using A::a;
cin >> a;
```



- **using编译指令**

```c++
using namespace 名字空间名;
```

将该名字空间中的成员加入到当前作用域，在此作用域中引用该名字空间的成员不需要加名字空间名的限定



main函数中可用

```c++
int main()
{
    using namespace A;
    //main函数中可用
}
```



文件中所有函数可用

```c++
//文件中所有函数可用
using namespace A;
    
int main()
{
    ...
}
```



## 对象和类

### 抽象和类

类和结构的区别

struct默认是公有的，class默认是私有的



### 对象构造

构造函数可以重载，也可以用缺省值，来实现不同的参数组来构造

可以通过列表初始化

```c++
class CExample {
public:
    int a;
    float b;
    const int c;
    //构造函数初始化列表，可以为常量初始化赋值，在构造函数内，常量不能赋值
    CExample(): a(0),b(8.8),c(10) {}
    
    //构造函数内部赋值
    CExample()
    {
        a=0;
        b=8.8;
        c=10;//常量不能这样赋值，会报错，因此在常量初始化时，应该用构造函数初始化列表
    }
};
```



### const对象

const对象里的值不可修改

```c++
const 对象名(初始化参数);
```

**const对象只能调用const成员函数**



#### const成员函数

const函数格式

```c++
int getx() const { return x; }
```

**const成员函数不可修改数据成员**



**在设计类的时候，不修改数据成员的成员函数都加上const！！！**



### this指针

每个类对象的普通函数（非静态成员函数）里都有一个隐藏的参数，就是this指针

一般用在返回值时，做链式调用（返回自身）

```c++
return *this; // 返回*this引用，支持链式调用
```



### 类作用域的常量

所有对象共享的常量



用关键字static

```c++
class salary {
    static const int month = 12;
}
```



## 使用类

### 运算符重载

使对象能用运算符操作

例如：类A的对象a1, a2, a3可以执行 a3 = a1 + a3

不能创建新的运算符，只能重载



operator后面跟着要重载的运算符

如：A类的加法函数原型

```c++
A operator+(const A &a) const;	//等价于 *this + a

bool operator>(const A &a) const;	//等价于*this > a
```

编译器中

```c++
t3 = t1 + t2;

//相当于调用了t1的operator+这个函数，并将t2作为参数
t3 = t1.operator+(t2);
```



### 友元

类的朋友，允许访问私有成员



使用friend关键字



#### **友元函数的应用**

主要用于运算符重载

```c++
class Time
{
    friend Time operator+(const Time & t1, const Time & t2);  //友元函数声明

private:
	int hours;
	int minutes;
public:
	Time();
	Time(int h,intm=0);
    
	void AddMin(int m);
	void AddHr(int h);
	void Reset(int h = 0, int m = 0);
    
	void Show() const;
};

Time operator+(const Time &t1, const Time &t2);	//全局的运算符重载函数


//因为是友元，因此可以访问私有成员
Time operator+(const Time &t1, const Time &t2)
{
    Time sum;
	sum.minutes = t1.minutes + t2.minutes;
	sum.hours = t1.hours + t2.hours + sum.minutes / 60;
	sum.minutes %= 60;
	return sum;
}
```

这种全局的运算符重载函数，在编译器中

```c++
t3 = t1 + t2;

//相当于调用了operator+这个全局函数，并将t1, t2作为参数
t3 = operator+(t1, t2);
```





重载输出运算符

```c++
#include <iostream>

class Fraction {
private:
    int numerator;
    int denominator;

public:
    Fraction(int num, int denom) : numerator(num), denominator(denom) {}

    // 友元函数声明
    friend std::ostream& operator<<(std::ostream& os, const Fraction& f);
    friend std::istream& operator>>(std::istream& is, Fraction& f);

    // 其他成员函数...
};

// 输出运算符重载
std::ostream& operator<<(std::ostream& os, const Fraction& f) {
    os << f.numerator << "/" << f.denominator;
    return os;	//这样可以作为左值，调用连续输出
}

// 输入运算符重载
std::istream& operator>>(std::istream& is, Fraction& f) {
    is >> f.numerator >> f.denominator;
    return is;
}

int main() {
    Fraction f1(1, 2);
    std::cout << "f1: " << f1 << std::endl;  // 使用友元输出运算符
    std::cin >> f1;                         // 使用友元输入运算符
    return 0;
}
```



### 运算符重载 - 成员函数或非成员函数

重载成成员函数

```c++
class Time
{
private:
	int hours
	int minutes;
public:
    Time();
    Time(int h,int m=0);
    
    void AddMin(intm);
    void AddHr(int h);
    void Reset(int h = 0, int m = 0);
    
    Time operator+(const Time & t) const;
        
    void Show() const;
};

Time t1(3,7), t2(1,20), t3;
int x = 2;

t3 = t1 + t2; 			// 正确	t3 = t1.operator+(t2);

t3 = 2 + t1;			// 错误	t3 = int.operator+(t1); 这是错误的，int类型里面没有operator+(t1)这个成员函数，因此报错

t3 = x + t1;			// 错误	t3 = int.operator+(t1); 这是错误的，int类型里面没有operator+(t1)这个成员函数，因此报错
```

重载成成员函数时，只有当第一个运算数是当前类对象时，才能找到重载的函数



**因此，当第一个运算数不是当前类对象时，不能重载成成员函数**



重载成全局函数

```c++
class Time
{
    friend Time operator+(const Time & t1, const Time & t2) const;
private:
	int hours
	int minutes;
public:
    Time();
    Time(int h,	int m=0); //重载的构造函数，带缺省参数
    
    void AddMin(intm);
    void AddHr(int h);
    void Reset(int h = 0, int m = 0);
        
    void Show() const;
};

Time t1(3,7), t2(1,20), t3;
int x = 2;

t3 = t1 + t2; 			// 正确	t3 = t1.operator+(t2);

t3 = 2 + t1;			// 正确	t3 = operator+(2, t1); 	等价于t3 = operator+(Time(2), t1);	int类型作为Time类的构造函数参数

t3 = x + t1;			// 正确	t3 = operator+(x, t1); 	等价于t3 = operator+(Time(x), t1);	int类型作为Time类的构造函数参数
```

**建议 operator+ 这样第一个运算数未必是当前类对象的函数，重载成全局函数**



operator+=

```c++
class Time
{
private:
	int hours
	int minutes;
public:
    Time();
    Time(int h,int m=0);
    
    void AddMin(intm);
    void AddHr(int h);
    void Reset(int h = 0, int m = 0);
    
    Time &operator+=(const Time & t);
        
    void Show() const;
};

Time &operator+=(const Time & t)
{
    minutes += t.minutes;
	hours += t.hours + minutes / 60;
	minutes %= 60;
	return *this;
}

Time t1(3,7), t2(1,20), t3;
int x = 2;

t3 += t1; 			// 正确	t3 = t3.operator+=(t1);

x += t1;			// 错误	int = int.operator+=(t1); 	这是错误的，int类型里面没有operator+=(t1)这个成员函数，因此报错
```

**像operator+=这样左值一定要是当前类对象，重载成成员函数**



**总结**



- **左边第一个运算数必须是当前类对象时，重载成成员函数**

- **当第一个运算数一定不能是当前类对象时，重载成全局函数**

- **当运算数仅仅是用于参数输入，重载成全局函数**



### 类的类型转换

#### 内置类型到类类型的转换

通过构造函数

只要有带一个参数的构造函数，就能实现参数类型到类类型的转换

```c++
class Time
{
    friend Time operator+(const Time & t1, const Time & t2) const;
private:
	int hours
	int minutes;
public:
    Time();
    Time(int h,	int m=0); //重载的构造函数，带缺省参数
    
    void AddMin(intm);
    void AddHr(int h);
    void Reset(int h = 0, int m = 0);
        
    void Show() const;
};

Time t1(3,7), t2(1,20), t3;
int x = 2;

t3 = 5; 				// t3 = Time(5);

t3 = 2 + t1;			// t3 = operator+(2, t1); 	等价于t3 = operator+(Time(2), t1);	int类型作为Time类的构造函数参数
```



#### 类类型到其他类类型的转换

通过类型转换函数实现

类型转换函数必须重载成成员函数



类型转换函数的格式

```c++
operator 目标类型名() const
{
    return (结果为目标类型的表达式)
}
```



示例：Time到int的转换函数定义

```c++
operator int() const
{
    return (int(hours))
}
```



使用：类型转换

```c++
int x;
x = t1;
x = (int)t1;
```



## 类和动态内存分配



### 拷贝构造与赋值运算符重载

**数据成员包含动态变量（例如指针，指针指向的空间是动态的）时，必须定义拷贝构造函数和赋值运算符重载函数！！！**

```c++
class String {
    char *data;		//指针之间不能直接拷贝赋值，因此需要重载拷贝构造函数
    int len;
public:
    String(const char *s = "");
    String(const String& other);	//拷贝构造函数
    
    ~String() { delete data;}
    String &operator=(const String& other);		//赋值运算重载函数（赋值运算只能重载为成员函数）
    
    friend String operator+(const String& s1, const String& s2);
    friend bool operator==(const String& s1, const String& s2);
    friend ostream operator<<(ostream& os, const String& s);
}
```

方法定义

```c++
String::String(const String &other)
{
    len = other.len;
	data = new char[len+1];
	for (int i = 0; i < len;++i)
        data[i] = other.data[i];
    data[len] = '\0';
}

String &String::operator=(const String &other)
{
    if(this== &other) return*this;	//检查是否是自己赋给自己，最彻底的办法就是检查内存地址是否一致
    
    delete data;	//长度不一定相同，因此先释放掉，再重新申请空间
    
    len = other.len;
    data = new char[len+1];
    for (int i=0;i<len;++i)
        data[i] = other.data[i];
    data[len] = '\0';
    return *this;
}
```



### 静态数据成员

整个类所有对象共享的变量（其他类看不到）

定义方法

成员前加static

静态成员变量不属于对象，而属于类的一部分

静态数据成员属于类，因此定义对象时并不为静态成员分配空间



类定义文件（.h）中不给初始值，只声明

```c++
class StaticSample {
private:
    static int obj_count;
}
```

**静态成员变量在类实现文件（.cpp）中分配空间**

```c++
#include "StaticSample.h"

int StaticSample::obj_count = 10;	//	在类实现中给初始值

StaticSample::StaticSample()
{
    ...
}
```



使用

类名::静态成员变量

对象名.静态成员变量



### 静态成员函数

专门处理静态数据成员，不能处理其他数据成员的函数

函数原型前加static



静态成员函数没有this指针



使用

类名::静态成员函数

对象名.静态成员函数



### 队列

一种特殊的线性表，插入在表尾，删除在表头



## 类继承



### 继承

优点：

代码复用

可以重用一个实现不公开的类



单继承格式

```c++
struct 派生类名: 派生方法 基类名
{
    新增的数据成员和成员函数;
}
```



派生方法

public：基类的公有成员成为派生类的公有成员；派生类的方法不能访问基类私有成员



#### 构造函数

如果基类有无参构造函数，那么可以不用显式调用，如果基类需要初始化，则必须显式调用

类定义

```c++
class RatedPlayer : public TableTennisPlayer
{
private:
    unsigned int rating;
public:
    //构造函数
    RatedPlayer(unsigned int r=0, const string& fn="none", const string& ln="none", bool ht=false);
    RatedPlayer(unsigned int r, const TableTennisPlayer& tp);
}
```

类实现

```c++
//构造函数列表初始化

//用派生类的参数构造基类
RatedPlayer::RatedPlayer(unsigned int r, const string& fn, const string& ln, bool ht) : TableTennisPlayer(fn, ln, ht)
{
    rating = r;
}

//拷贝构造基类
RatedPlayer::RatedPlayer(unsigned int r, const TableTennisPlayer& tp) : TableTennisPlayer(tp), rating(r)
{
}
```



### 重新定义基类的函数

函数原型与基类完全一致

```c++
//重新定义基类函数
void BrassPlus::ViewAcct(double amt) const
{
    //可以调用基类的函数
    Brass::ViewAcct(amt);
}
```



派生类重定义的函数覆盖了基类的同名函数，即对派生类对象调用这两个函数时，调用的是派生类重定义的函数



### 多态与公有继承

#### 多态 - 虚函数



**virtual关键字**

当基类指针指向的派生类对象，并对指针调用虚函数时，**会到派生类中去寻找同原型的函数并执行。如果不存在，则执行基类的函数**

派生类中virtual可以不加，编译器默认**与基类虚函数同名的函数也是虚函数**



构造函数不能是虚函数

析构函数建议是虚函数，除非不会被当作基类使用

虚函数具有继承性



### protected成员

一类特殊的私有成员，可以被派生类的成员函数访问，提高派生类成员函数访问基类数据成员的效率



### 抽象基类

#### 纯虚函数

在基类中说明的虚函数，它在该基类中没有定义，但要在它的派生类里定义自己的版本，或重新说明为纯虚函数

纯虚函数声明

```c++
virtual 类型 函数名(参数表) = 0;
```

如果一个类中至少有一个纯虚函数，则该类被称为抽象类



抽象类只能作为基类，不能建立抽象类的对象

可以声明指向抽象类的指针或引用，此指针可指向它的派生类，进而实现多态性

抽象类不能用作参数类型、函数返回类型或显式转换类型

如果派生类中给出了基类所有纯虚函数的实现，则该派生类不再是抽象类，否则仍为抽象类



## C++中的代码重用



### 包含对象成员的类

对象成员的初始化由构造函数的初始化列表完成

```c++
//类定义中
date birthday;

//类声明中
student(const string& n, int yy, int mm ,int dd): birthday(yy, mm, dd)
{
    name = n;
	coursenum = 0;
}
```



### 私有继承

基类的公有成员和保护成员在派生类中都是私有成员

即，基类的方法不再是派生类接口的一部分，但派生类的成员函数可以使用它们



**与将对象作为成员的功能相同**

成员对象：命名的对象

私有继承：未命名的基类对象



构造函数实现

在派生类的构造函数中调用基类的构造函数

```c++
//通过私有继承的方式
student(const string& n, int yy, int mm ,int dd): date(yy, mm, dd)
{
    name = n;
	coursenum = 0;
}
```



派生类可以直接强制转换为基类对象，相当于把基类部分抽取出来

```c++
//强制转换为基类
date(student);
```



### 多重继承

从多个基类派生

格式

```c++
class 派生类名: 派生方法 基类名1, 派生方法 基类名2, ...{
    ...
};
```



#### 区分不同基类继承的同名函数

在派生类中重新封装同名函数

```c++
class A{
public:
	void f();
}

class B {
public:
    void f();
    void g();
}

class C: public A, public B {
public:
    void g();
    void h();
    void fA() { A::f(); }
    void fB() { B::f(); }
};
```



#### 从不同基类中继承了同一个类的多个实例

```c++
class people {
    ...
}
class teacher: public people {
    ...
}
class doctor: public people {
    ...
}

class teacher_doctor: public teacher, public doctor {
    ...
}
```

没必要有两个people类的示例



**通过 虚基类 解决**

将多个类（共同基类）派生的对象只有一个基类对象

共同派生时共享一个基类副本



格式

派生方法前加关键字virtual

```c++
class people {
    ...
}
class teacher: virtual public people {
    ...
}
class doctor: virtual public people {
    ...
}

class teacher_doctor: public teacher, public doctor {
    ...
}
```

people是teacher和doctor的**虚基类**



**虚基类由最终的派生类直接构造**

teacher_doctor构造函数写法

```c++
teacher_doctor(参数表): people(参数表), teacher(参数表), doctor(参数表)
{
    ...
}
```



### 类模板

#### 定义及使用

```c++
template <typename T>
class Sample {
    Sample(const T& t);
 
}

//使用
Sample<int> intSample(5);
Sample<double> doubleSample(2.5);
```

