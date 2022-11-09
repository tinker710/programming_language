[toc]
# 指针（pointer）
## 运算符 &
1. scanf("%d", &i); 里的&
2. 获得变量的地址，它的操作数必须是变量
## 指针
就是保存地址的变量
```
int i;
int* p = &i;
int* p,q;
int *p,q;
``` 
### 指针变量
1. 变量的值是内存的地址
   1. 普通变量的值是实际的值
   2. 指针变量的值是具有实际值的变量的地址
### 访问那个地址上的变量 *
- *是一个单目运算符，用来访问指针的值所表示的地址上的变量
- 可以做右值也可以做左值
  - int k = *p
  - *p = k + 1
### 作为参数的指针
- void f(int *p);
- 在被调用的时候得到了某个变量的地址；
  - int i=0; f(&i);
- 在函数里面可以通过这个指针访问外面的这个i
```
#include <stdio.h>
void f(int *p);

int main(void)
{
    int i=6;
    printf("&i=%p\n", &i);
    f(&i);

    return 0;
}

void f(int *p)
{
    printf("p = %p\n",p);
}

```
## 指针应用场景
### 场景一 swap
```
#include<stdio.h>

void swap(int *pa, int *pb);

int main(void)
{
    int a = 5;
    int b = 6;
    swap(&a, &b);
    printf("a=%d, b=%d\n,a,b);

    return 0;
}

void swap(int *pa, int *pb)
{
    int t = *pa;
    *pa = *pb;
    *pb = t;
}
```
### 场景二 
函数返回运算的状态，结果通过指针返回
```
#include<stdio.h>
/**
@return 如果除法成功，返回1；否则返回0.
*/

int divide(int a, int b, int *result);

int main(void)
{
  int a = 5;
  int b = 2;
  int c;
  if (divide(a,b,&c)){
    printf("%d/%d = %d\n",a,b,c);
  }
  return 0;
}

int divide(int a, int b, int *result)
{
  int ret = 1;
  if (b==0) ret = 0;
  else{
    *result = a/b;
  }
  return ret;
}
```
## 传入函数的数组成了什么？
- 函数参数表中的数组实际上是指针
  - sizeof(a) == sizeof(int *)
  - 但是可以用数组的运算符[]进行运算
### 数组变量是特殊的指针
- 数组变量本身表达地址，所以
  - int a[10]; int *p = a; //无需用&取地址
  - 但是数组的单元表达的是变量，需要用&取地址
  - a == &a[0]
- []运算符可以对数组做，也可以对指针做：
  - p[] <==> a[0]
- 运算符可以对指针做，也可以对数组做
- 数组变量是const指针，所以不能被赋值
  - int a[] <==> int * const a=
## 动态内存分配
```
int *a = (int *)malloc(n*sizeof(int))
```
需要include <stdlib.h>
```
#include<stdio.h>
#include<stdlib.h>

int main(void)
{
	int number;
	int i;
	int* a;
	printf("输入数量：");
	scanf("%d", &number);
	// int a[number];
	a = (int*)malloc(number*sizeof(int));
	for (i=0; i<number; i++){
		scanf("%d",&a[i]);
	}
	for (i=number-1; i>=0; i--){
		printf("%d",a[i]);
	}
	free(a);
	return 0;
 } 
```
### malloc
void* malloc(size_t size);
- 向malloc申请的空间的大小是以字节为单位的
- 返回的结果是void*，需要类型转换为自己需要的类型
- (int*)malloc(n*sizeof(int))
#### 没空间了？
- 如果申请失败则返回0，或者叫做NULL
- 你的系统能给你多大的空间？
```
#include<stdio.h>
#include<stdlib.h>

int main(void)
{
	void *p;
	int cnt = 0;
	while ((p = malloc(100*1024*1024))){
		cnt++;
	}
	printf("分配了%d00MB的空间\n",cnt);
	return 0;
} 
```
#### free()
- 把申请得来的空间还给“系统”
- 申请过的空间，最终都应该要还
  - 混出来的，迟早都是要还的
- 只能还申请来的空间的首地址

- **常见问题**
  - 申请了没有free -> 长时间运行内存逐渐下降
    - 新手：忘了
    - 老手：找不到合适的free时机
  - free过了再free
  - 地址变过了，直接去free

# 字符串
## 字符数组
char word[] = {'H','e','l','l','o','!'};
## 字符串
char word[] = {'H','e','l','l','o','!','\0'};
- 以0（整数0）结尾的一串字符
  - 0或'\0'是一样的，但是和'0'不同
- 0标志字符串的结束，但它不是字符串的一部分
  - 计算字符串长度的时候不好含这个0
- 字符串以数组的形式存在，以数组或指针的形式访问
  - 更多的是以指针的形式
- string.h里有很多处理字符串的函数
  1. char *str = "Hello";
  2. char word[] = "Hello";
  3. char line[10] = "Hello";
### 字符串常量
- "Hello"
- "Hello"会被编译器变成一个字符数组放在某处，这个数组的长度是6，结尾还有表示结束的0
- 两个相邻的字符串常量会被自动连接起来
### 字符串
- c语言的字符串是以字符数组的形态存在的
  - 不能用运算符对字符串做运算
  - 通过数组的方式可以遍历字符串
- 唯一特殊的地方是字符串字面量可以用来初始化字符数组
- 以及标准库提供了一系列字符串函数
### 字符串常量
char* s = "Hello, world!";
- s是一个指针，初始化为指向一个字符串常量
  - 由于这个常量所在的地方，所以实际上s是const char* s，但是由于历史的原因，编译器接受不带const的写法
  - 但是试图对s所指的字符串做写入会导致严重的后果
- 如果需要修改字符串，应该用数组：
  char s[] = "Hello, world!";
### 指针还是数组？
char *str = "hello";
char word[] = "hello";
- 数组：这个字符串在这里
  - 作为本地变量空间自动被回收
- 指针：这个字符串不知道在哪里
  - 处理参数
  - 动态分配空间
- 如果要构造一个字符串：数组；如果要处理一个字符串：指针。
### 字符串赋值？
```
char *t = "title";
char *s;
s = t;
```
并没有产生新的字符串，知识让指针s指向t所指的字符串，对s的任何操作就是对t做的
### 字符串输入输出
scanf读入一个单词（到空格、tab或回车为止）
## 字符串函数
### strlen
### strsmp
```
int mycmp(const char* s1, const char* s2)
{
  int idx = 0;
  while (s1[idx] == s2[idx] && s1[idx] != "\0"){
    // if (s1[idx] != s2[idx]){
    //  break;
    // }else if (s1[idx]) == '\0'){
    //  break;
    // }
    idx ++;
  }
  return s1[idx] - s2[idx];
}
```
### strcpy
- char * strcpy(char *restrict dst, const char *restrict src);
- 把src的字符串拷贝到dst
  - restrict表明src和dst不重叠
- 返回dst
  - 为了能链起代码来
```
char* mycpy(char* dst, const char* src)
{
  //int idx = 0;
  //while (src[idx] != '\0'){
  //  dst[idx] = src[idx];
  //  idx ++;
  //}
  //dst[idx] = '\0';
  //return dst;
  char* ret = dst;
  while (*dst++ = *src++)
    ;
  *dst = '\0';
  return dst;
}
```
### strcat
- char * strcat(char *restrict s1, const char *restrict s2);
- 把s2拷贝到s1的后面，接成一个长的字符串
- 返回s1
- s1必须具有足够的空间
strcpy和strcat都可能出现安全问题
- 如果目的地没有足够的空间？
安全版本
1. char * strncpy(char *restrict dst, const char *restrict src, size_t n);
2. char * strncat(char *restrict s1, const char *restrict s2, size_t n);
3. int strncmp(const char *s1, const char *s2, size_t n);
### 字符串中找字符串 
1. strchr
2. strrchr
3. char * strstr(const char *s1, const char *s2);
4. char * strcasestr(const char *s1, const char *s2);
### 常量符号化
用符号而不是具体的数字来表示程序中的数字
## 枚举
1. 枚举是一种用户定义的数据类型，它用关键字**enum**以如下语法来声明：
enum 枚举类型名字{名字0,...,名字n}；
2. 枚举类型名字通常并不真的使用，要用的是在大括号里的名字，因为它们就是常量符号，它们的类型是int，值则依次从0到n。如：
enum colors{red,yellow,green};
3. 就创建了三个常量，red的值是0，yellow是1，而green是2。
4. 当需要一些可以排列起来的常量值时，定义枚举的意义就是给了这些常量值名字。
```
#include<stdio.h>
enum color{red,yellow,green};
void f(enmu color c);
int main(void)
{
  enum color t = red;
  scanf("%d", &t);
  f(t);
  return 0;
}

void f(enum color c)
{
  printf("%d\n",c);
}
```
- 枚举量可以作为值
- 枚举类型可以跟上enum作为类型
- 但是实际上是以整数来做内部计算和外部输入输出的
