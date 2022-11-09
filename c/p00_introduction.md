[toc]
# 1. 介绍
## 解释型和编译型
1. 解释型：借助一个程序，那个程序能试图理解你的程序
2. 编译型：借助一个程序，把你的程序翻译成计算机能够理解的语言

### 几点
1. 语言本无编译/解释之分
2. 只是常用的执行方式
3. 解释型语言有特殊的计算能力
4. 编译型语言有确定的运算能力
   
## 入门程序
```c
#include <stdio.h>

int main()
{
    printf("%d",12+34);
    return 0;
}
```

# 2. 变量
```
int price;
scanf("%d", &price)
```
## 变量名
只能由字母，数字和下划线组成，数字不可以出现在第一个位置，关键字不可以用作标识符。

## 常量
```
const int a = 0;
```
## 数据类型
1. 整数 int
   1. 两个整数的计算结果只能是整数
2. 带小数点的数
   1. float
   2. double
    ```
    scanf("%lf", &a)
    ```
# 3. 表达式
## 运算符
取余 %
## 算子
- 例子，求平均
  ```
  int a,b;
  scanf("%d","%d", &a, &b);
  double c = (a+b)/2.0;
  printf("%d和%d的平均值为：%f\n",a,b,c);
  ```
## 运算符
1. 单目高于双目高于赋值符
2. 赋值作为运算，赋值结果也是有结果的
### 结合关系
1. 一般自左向右
2. 单目+-和赋值=自右向左
### 复合赋值
+=
-=
++递增
--递减
#### a++，++a
| 表达式 | 运算 | 表达式的值  |
| -----  | ---  |  -------- |
| a++    | 给a+1| a原来的值  |
| ++a    | 给a+1| a+1以后的值|
## 断点调试

# 4. if
```
#include <stdio.h>
int main()
{
  int x;
  scanf("%d",&x);

  int f=0;
  if (x <0){
    f = -1;
  }else if (x == 0){
    f = 0;
  }else if (x > 5){
      f = 2*x
  }else{
      f = 3*x
  }
  printf("%d", f)
  return 0;

}
```
## 关系运算符
1. ==
2. !=
3. \>
4. \>=
5. <
6. <=
所有的关系运算符的优先级比算术运算符低，但是比赋值运算高
## 注释
**//** 单行注释
**/\* \*/** 多行注释
## 多路分支switch-case
```
switch (常量表达式){
  //常量表达式必须是int
case 常量：
  语句
  ······
case 常量：
  语句
  ······
default:
  语句
  ······
}

```
# 5. 循环
## 5.1 while
## 5.2 do-while
int a = rand()
b = a % 100
## 5.3 for
```
for (i = 1; i<=n;i++){
  //初始条件，循环继续条件，循环每一轮要做的动作
  fact *= i;
}
```
## Tips for loops
1. 如果有固定次数，用for
2. 如果必须执行一次，用do-while
3. 其它情况用while
## 循环控制
break：跳出循环
continue：跳过循环这一轮剩下的语句进入下一轮
## 循环嵌套
### goto
跳到指定标号
goto out;
语句
out：
  return 0；
# 6. 数据类型
## C语言的类型
1. 整数
   1. char、short、int、long、longlong
2. 浮点数
   1. float、double、long double
3. 逻辑
   1. bool
4. 指针
5. 自定义类型
6. 
## 强制类型转换
```
int i = 32768;
short s = (short)i;
```

强制类型转换的优先级高于四则运算
## bool
1. #include <stdbool.h>
2. 之后就可以使用bool和true、false
```
# include <stdio.h>
# include <stdbool.h>

int main()
{
  bool b = 6>5;
  bool t = true;
  t = 2;
  printf("%d\n",b)
  return 0;
}
```

# 7. 逻辑运算
| 运算符 |描述|
| ------ |  ---  |
|  ！    | 逻辑非 |
|    &&  | 逻辑与 |
|  \|\|  | 逻辑或 |
# 8. 函数
## 8.1 函数的定义和使用
 
 1. 函数头（返回类型 函数名 （参数表））
 2. 函数体
## 函数原型
- 函数头，以分号“；”结尾，就构成了函数的原型
- 函数原型的目的是告诉编译器这个函数长什么样
  - 名称
  - 参数（数量及类型）
  - 返回类型
## 参数传递
- 如果函数有参数，调用函数时必须传递给他数量、类型正确的值
- 可以传递给函数的值是表达式的结果，包括：
  - 字面量
  - 变量
  - 函数的返回值
  - 计算的结果

### 本地变量
- 生存期
- 作用域
- 本地变量是定义在块（大括号）内的

# 9. 数组
int number[100];
```
#include <stdio.h>
int main()
{
  int x;
  double sum = 0;
  int cnt = 0;
  int number[100];
  scanf("%d",&x);
  while (x != -1){
    number[cnt] = x;
      //
      {
        int i;
        printf("%d\t",cnt);
        for (i=0; i<= cnt; i++){
          printf("%d\t", number[i]);
        }
        printf("\n");
      }
      //
    sum += x;
    cnt ++;
    scanf("%d", &x);
  }
  if (cnt > 0){
    printf(%f\n, sum/cnt);
    int i;
    for (i = 0; i<cnt; i++){
      if (number[i] > sum/cnt){
        printf("%d\n", number[i]);
      }
    }
  }
  return 0;
}
```
## 9.1 定义数组
1. <类型>变量名称[元素数量]；
   1. int grades[100];
   2. double weight[20];
2. 元素数量必须是整数
3. c99之前：元素数量必须是编译时刻确定的字面量


- 数组是一种容器，特点是：
  - 其中所有的元素具有相同的数据类型；
  - 一旦创建，不能改变大小
  - *（数组中的元素在内存中是连续依次排列的）
## 9.2 数组的集成初始化
```
int a[] = {2,4,6,7,1,3,5,9,11,13,23,14,32};
int a[13] = {2}
int a[13] = {0}
int a[13] = {[1] = 2, [5] = 6}
sizeof(a)/sizeof(a[0])
```
## 9.3 二维数组
int a[3][5];
a[i][j]表示第i行，第j列
