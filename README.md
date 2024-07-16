# C++学习笔记

## 处理数据

### 整型

C++提供多种整型，能够根据程序的具体要求选择最合适的整型

- 符号类型（正负值的取值范围几乎相同）：short、int、long、long long

- 在C++中，**并没有规定每一类整型要占多少空间，只是规定了至少要占多少空间**

  short：**至少占16位**

  int：至少与short一样长

  long：**至少32位**，且不短于int

  long long：**至少64位**，且不短于long

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

  **十进制默认都是int**

  L或I：长整型。如100L
  U或u：无符号数。如100U
  LU或UL：无符号长整型
  LL或ll：long long类型
  LLU或uLL：无符号long long类型

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

**true是1，false是0**

可以作为算术运算的运算数

