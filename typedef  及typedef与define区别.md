# typedef定义
typedef是在C和C++编程语言中的一个关键字。作用是为现有的数据类型(int、float、char……)创建一个新的名字，目的是为了使代码方便阅读和理解。

# typedef用法

### 对于数据类型使用例如：

```cpp
typedef  int   NEW_INT;
```

以上就是给int起了一个新的名字NEW_INT，注意要加分号。当要定义int类型数据时就可以：

```dart
NEW_INT num;
```

此时NEW_INT num 等同于 int num。
### 2、对于指针的使用例如
~~~
typedef  int   *PTRINT;
~~~
以上就是给int *起了一个新的名字NEW_INT。可定义int类型指针变量如：

~~~
PTRINT x;
~~~
此时PTRINT x等同于int *x。

3、对于结构体的使用
在声明结构体时可为结构体和结构体指针起别名，如：

~~~
typedef struct NUM
{
     int a;
     int b;
}DATA,*PTRDATA;
~~~
此时DATA等同于struct NUM，*PTRDATA等同于struct NUM *。

定义结构体变量及指针可简化为：
~~~
   DATA data;           //定义结构体变量
 
   PTRDATA pdata;   //定义结构体指针
 ~~~
举个例子：
~~~

#include <stdio.h>
 
typedef struct NUM
{
     int a;
     int b;
}DATA,*PTRDATA;
 
int main()
{
       DATA data;           //定义结构体变量
       PTRDATA pdata;   //定义结构体指针
       pdata=&data;      //结构体指针指向结构体变量      
 
       data.a=100;
       data.b=500;
 
       printf("a=%d\nb=%d\n",data.a,data.b);
       printf("a=%d\nb=%d\n",pdata->a,pdata->b);
       return 0;
}
~~~
# typedef 与 define 区别
**Typedef是起别名，define是替换。**

例如：

```cpp
typedef int *PTR; PTR a,b;
```

此时a,b都是指针变量。

```less
#define PTR int* PTR a,b;
```

此时等同于

```less
int *a,b;
```

只有a为指针变量，而b为整型变量。

