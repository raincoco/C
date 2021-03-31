# C/C++ 笔记

这是我的C语言学习笔记，记录一些我自己的学习经历和一些遇到的问题。

## C语言基础
### 一、字符和字符串
#### 1、字符串是结尾为'\0'的数组。
#### 2、关于字符和字符串引号的使用：
* 字符类型只能用单引号' '。
* 字符串类型用双引号" "（结尾为'\0'的数组）。
```c
char ch = 'A';
char str[10] = "Hello";
```
### 二、数组
数组字符串初始化:memset。
### 三、结构体
结构体数组每一个元素才是结构体。

### 四、动态内存
#### 1、内存分配操作
malloc函数：分配连续的内存空间。<br>
```c
void *malloc(size_t size);
返回值：成功返回分配的内存空间指针，失败返回空指针BULL
```
free函数：释放内存，内存使用完后一定要调用free释放内存。<br>
```c
void free(void *ptr);
```
2、内存分配可能出现的问题
内存耗尽：分配空间使用完毕后一定要及时释放内存。<br>
野指针：无效指针。<br>
>野指针产生原因：<br>
>1、定义指针未初始化。<br>
>2、指针释放后未置空； 释放内存后应将指针置位0。<br>
### 五、文件操作
#### 1、文件指针定义
```c
FILE *fp;
```
#### 2、文件操作函数<br>
>fopen()：打开文件。<br>
>fclose()：关闭文件，释放内存（文件使用完后一定要关闭文件释放内存！）。<br>

>fprintf()：向文件中写入数据。<br>
>fgets()：从文件中读取数据。<br>
>fputs()：向文件中写入数据。<br>

>fwrite()：向二进制文件写入数据。<br>
>fread()：从二进制文件读取数据。<br>

文件定位<br>
>ftell：返回当前文件位置指针的值。<br>
>rewind：将文件位置指针移动到文件开头。<br>
>fseek：将文件指针移动到人任意位置。<br>

#### 3、文件缓冲区
调用fputs、fwrite等函数向文件写入数据时，数据不会立即写入磁盘文件，而是先写入缓冲区文件，等缓冲区写满后才写入磁盘文件。调用fclose时也会将把缓冲区数据写入文件。<br>
>fflush：可以立即将缓冲区数据写入文件。<br>

### 六、目录操作
#### 1、目录指针定义
```c
DIR *dir;
```
#### 2、目录函数
头文件
```c
#include<dirent.h>
```
>opendir()：打开目录函数。<br>
>closedir()：关闭目录函数，一定要关闭目录！<br>
>readdir()：读取目录函数，返回一个结构体，包含读取到的文件和目录的信息。<br>
>>readdir返回的结构体重包含了文件和目录信息。如文件名、文件类型等。<br>

>access：判断当前操作系统用户对文件或目录的存取权限。（头文件unistd.h（unix的库））<br>
>utime()：有结构体utimbuf，修改文件的存取时间和修改时间。<br>
>remane()：修改文件或目录名称。<br>
>remove()：删除文件或目录。<br>
>stat结构体：存放文件或目录的状态信息。 <br>

### 七、函数
#### 1、编译预处理
1）include：包含文件，<>标准头文件；""指定目录文件（自己写的文件），可以加入.C的文件。<br>
2）define：定义宏。<br>
>无参数宏：相当于替换；<br>
>带参数宏；<br>
3）条件编译：ifdef和ifndef，在预编译的时候判断。ifndef，用来防止重复包含头文件。<br>
#### 2、main函数参数：argc,argv,envp
```c
int main(int argc,char *argv[],char *envp[])
```
>argc：存放命令行参数个数。<br>
>argv：字符串数组，每个元素都是一个字符指针，指向一个字符串，即命令行的每一个参数。<br>
>envp：字符串数组，每个元素都是一个字符指针，指向一个环境变量参数。<br>
#### 3、时间操作函数
>time()：返回从1970.1.1的0时0分0秒到现在的秒数。<br>

time_t数据类型：表示时间数据类型，是一个long（长整数）类型别名。头文件件time.h。表示一个日历时间，从1970.1.1的0时0分0秒到现在的秒数。<br>
tm结构体：方便表示时间的结构体。<br>
localtime库函数：把time_t表示的时间转换为结构体tm表示的时间。<br>
mktime库函数：把结构体tm表示的时间转为time_t表示的时间。进行时间运算时time_t整数比字符串好用。<br>

程序睡眠：<br>
头文件unistd.h（该函数库是unix的库）<br>
```c
#include<unistd.h>
```
>sleep()：程序睡眠，单位秒；<br>
>usleep()：程序睡眠，单位微秒。<br>
 
计时器：
头文件sys/time.h（该函数库是unix的库）<br>
```c
#include<sys/time.h>
```
timeval结构体：从1970.1.1到现在的秒数或微秒数。<br>
timezone结构体：时区结构体，与格林威时间差多少。<br>
gettimeofday库函数：从1970.1.1到现在的秒数，和当前秒已经逝去的微秒数。<br>
#### 4、系统错误函数
errno全局变量：库函数返回错误码会存入errno全局变量中，错误码对应的错误消息定义在errno.h头文件中。<br>
>strerror()：根据错误码显示错误描述。<br>
>perror()：用于在屏幕上显示最近一次错误码和消息描述。<br>

重点：<br>
>1）不是所有库函数失败都会设置errno值。不属于系统调用的函数不会设置errno。<br>
>2）errno不能作为调用库函数失败的标志。如果库函数正确的执行，那么errno的值不会被清零，只有库函数发生错误时才会设置。<br>
#### 4、printf输出函数
```c
printf("%d",*p);
```
输出整数型（%d）时，函数要求你提供一个整数型（int），而p是一个指针，填入p将把指针内的地址输出。<br>
```c
printf("%s",p);
```
输出字符串（%s）时，函数要求你提供一个指针，而p就是一个指针变量，可以直接写变量名p。<br>
#### 5、关于函数传入参数为一个指针
```c
void set(char* p);
```
该函数参数为一个char型指针p，当调用该函数时，我们需要传入的是一个指针变量p。即可以看作
```c
void set((char* ) p);
```
该函数需要一个（char* ）型的变量p（指针变量）。<br>
