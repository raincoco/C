
这是我的C语言学习笔记，记录一些我自己的学习经历和一些遇到的问题。

# C语言基础部分
## 一、字符和字符串
### 1、字符串是结尾为'\0'的数组。
### 2、关于字符和字符串引号的使用：
* 字符类型只能用单引号' '。
* 字符串类型用双引号" "（结尾为'\0'的数组）。
```c
char ch = 'A';
char str[10] = "Hello";
```
## 二、数组
数组字符串初始化:memset。
## 三、结构体
结构体数组每一个元素才是结构体。
### 四、函数
main函数参数：argc,argv,envp
>argc：存放命令行参数个数。<br>
argv：字符串数组，每个元素都是一个字符指针，指向一个字符串，即命令行的每一个参数。<br>
envp：字符串数组，每个元素都是一个字符指针，指向一个环境变量参数。<br>

### 6、动态内存
>malloc函数：分配连续的内存空间。<br>
free函数：释放内存。<br><br>
内存耗尽：分配空间使用完毕后一定要及时释放内存。<br>
野指针：无效指针。<br>
>>野指针产生原因：<br>
>>1、定义指针未初始化。<br>
>>2、指针释放后未置空； 释放内存后应将指针置位0。
### 7、文件操作
FILE 
>fopen：打开文件。
fclose：关闭文件，释放内存（文件使用完后一定要关闭文件释放内存！）。
fprintf：向文件中写入数据。
fgets：从文件中读取数据。
fwrite：向二进制文件写入数据。
fread：从二进制文件读取数据。

文件定位
ftell：放回当前文件位置指针的值。
rewind：将文件位置指针移动到文件开头。
fseek：将文件指针移动到人任意位置。

文件缓冲区
调用fprintf、fwrite等函数向文件写入数据时，数据不会立即写入磁盘文件，而是先写入缓冲区文件，等缓冲区写满后才写入磁盘文件。调用fclose时也会将把缓冲区数据写入文件。
fflush：可以立即将缓冲区数据写入文件。