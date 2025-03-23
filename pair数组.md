### 1.主要功能
     当两个数需要绑定在一起成为一个值时，可以通过pair数组实现，这两个数可以具有不同的数据类型。用pair的两个公有函数first second访问第一个数和第二个数。

eg：<1 , 2>中first是1，second是2   
<1 , 2.2>中first是1，second是2.2
### 2.如何定义(构造)
~~~
pair<int , int> p1;//默认构造函数
pair<int , double> p2(1,2.2)//用特定值初始化
pair<int , int> p3(p1);//通过复制p1构造函数
~~~
### 3.如何访问元素
~~~
pair<int , int> p1(1,2);
cout<<p1.first<<' '<<p1.second<<endl;
//输出结果：1 2
~~~
### 4.如何赋值
（1）用make_pair赋初值
~~~
pair<double , double> p1;
p1=make_pair(1.2,2.2);
~~~
  (2)  变量间赋值（数据类型相同才可以）

pair<int , double> p1(1,1.2);
pair<int , double> p2=p1;
### 5.sort如何对pair数组排序
      默认对 first 进行升序排列 ，当first相同时, 对second 进行升序排列。也可以自己写一个cmp 实现对其别的要求的排序 。
