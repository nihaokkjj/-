# 目录
[一、auto简介](https://blog.csdn.net/look_outs/article/details/129025156?ops_request_misc=%257B%2522request%255Fid%2522%253A%25227F7F0AC1-907E-4D77-BD41-A861D9505DBF%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=7F7F0AC1-907E-4D77-BD41-A861D9505DBF&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~top_positive~default-1-129025156-null-null.nonecase&utm_term=auto&spm=1018.2226.3001.4450#t0)

[二、auto的使用场景](https://blog.csdn.net/look_outs/article/details/129025156?ops_request_misc=%257B%2522request%255Fid%2522%253A%25227F7F0AC1-907E-4D77-BD41-A861D9505DBF%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=7F7F0AC1-907E-4D77-BD41-A861D9505DBF&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~top_positive~default-1-129025156-null-null.nonecase&utm_term=auto&spm=1018.2226.3001.4450#t1)

[三、注意事项](https://blog.csdn.net/look_outs/article/details/129025156?ops_request_misc=%257B%2522request%255Fid%2522%253A%25227F7F0AC1-907E-4D77-BD41-A861D9505DBF%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=7F7F0AC1-907E-4D77-BD41-A861D9505DBF&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~top_positive~default-1-129025156-null-null.nonecase&utm_term=auto&spm=1018.2226.3001.4450#t2)

[拓、范围for](https://blog.csdn.net/look_outs/article/details/129025156?ops_request_misc=%257B%2522request%255Fid%2522%253A%25227F7F0AC1-907E-4D77-BD41-A861D9505DBF%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=7F7F0AC1-907E-4D77-BD41-A861D9505DBF&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~top_positive~default-1-129025156-null-null.nonecase&utm_term=auto&spm=1018.2226.3001.4450#t3)

 [【总结】](https://blog.csdn.net/look_outs/article/details/129025156?ops_request_misc=%257B%2522request%255Fid%2522%253A%25227F7F0AC1-907E-4D77-BD41-A861D9505DBF%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=7F7F0AC1-907E-4D77-BD41-A861D9505DBF&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~top_positive~default-1-129025156-null-null.nonecase&utm_term=auto&spm=1018.2226.3001.4450#t4)

[【源代码】](https://blog.csdn.net/look_outs/article/details/129025156?ops_request_misc=%257B%2522request%255Fid%2522%253A%25227F7F0AC1-907E-4D77-BD41-A861D9505DBF%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=7F7F0AC1-907E-4D77-BD41-A861D9505DBF&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~top_positive~default-1-129025156-null-null.nonecase&utm_term=auto&spm=1018.2226.3001.4450#t5)
## 一、auto简介
1.是什么？

        auto是一个提示符，提示编译器根据变量的值来推导变量的类型。
        在早期C/C++中auto的含义是：使用auto修饰的变量，是具有自动存储器的局部变量，C++11中，标准委员会赋予了auto全新的含义即：auto不再是一个存储类型指示符，而是作为一个新的类型指示符来指示编译器，auto声明的变量必须由编译器在编译时期推导而得。

2.为什么？

        对于某些较长或较奇怪的数据类型，可交给编译器自行推导，这样使代码更简洁。

3.怎么用？

        定义变量使用auto可让编译器自动推导变量类型；和范围for使用来遍历数组；加引用和范围for一起使用来修改数值。

        使用auto定义变量时必须初始化，auto变量无法作为参数。在编译阶段编译器需要根据初始化表达式来推导auto的实际类型。因此auto并非是一种“类型”的声明，而是一个类型声明时的“占位符”，编译器在编译期会将auto替换为变量实际的类型。
## 二、auto的使用场景
1. 使用auto自动识别变量类型

eg. auto自动识别变量类型
![[Pasted image 20241102122159.png]]
eg. 当变量类型比较长时，auto自动识别变量类型，使代码变得简洁。
![[Pasted image 20241102122207.png]]
2. auto关键字经常和范围for一起使用，用来遍历数组。
![[Pasted image 20241102122219.png]]

注意，这里是将数组中的元素赋值给i，所以i的改变并不会影响原数组。

3. auto结合引用和范围for一起使用，用来修改数组。
![[Pasted image 20241102122254.png]]


## 三、注意事项
1.使用auto声明变量必须初始化。
![[Pasted image 20241102122357.png]]

2.不能使用auto和指针结合来修改数组。

         auto* a 加一个 * 是在强调变量 a 是指针，故a只能接受指针类型，并不是将变量类型改为指针类型，没有指针auto类型。

eg. auto* 只能接收指针类型。
![[Pasted image 20241102122559.png]]
eg. auto* aa 并没有使 变量aa的类型变为int **。
![[Pasted image 20241102122612.png]]

可使用操作符typeid(a).name()来查看变量a的数据类型。(注意typeid不是函数)

3.同理，auto& b 是在强调b是引用，但引用可以除了可以接收引用，还可以接收其它类型，故b除了可以接收引用外还可以接收其它类型（int, double……），说明b是该类型变量的引用。

4.同句中的auto的类型必须相同。
![[Pasted image 20241102122633.png]]
5.auto不能作为参数。
 ![[Pasted image 20241102122714.png]]

拓、范围for
1. 是什么？

        范围for全称基于范围的for循环，是C++11中引入的一种新特性，它允许程序员更简洁地遍历序列（如数组、字符串等）中的元素。

2. 为什么？

        对于一个有范围的集合而言，由程序员来说明循环的范围是多余的，有时候还会容易犯错误，因此 C++11 中引入了基于范围的for循环。

3. 怎么用？

        for 循环后的括号由冒号“ ：”分为两部分：第一部分是范围内用于迭代的变量，第二部分则表示被迭代的范围。
        
![[Pasted image 20241102122815.png]]
4. 注意事项：
a) 范围for的范围必须是确定的:
![[Pasted image 20241102122833.png]]


 ## 总结
![[Pasted image 20241102122906.png]]
## 源代码
~~~
#include<iostream>
using std::cout;
using std::endl;
 
int main()
{
	//auto a = 1;
	//auto b = 3.14;
	//auto c = "a";
	//auto d = 'a';
 
	1.auto自动识别类型
	//cout << typeid(a).name() << endl; //typeid()识别变量类型
	//cout << typeid(b).name() << endl;
	//cout << typeid(c).name() << endl;
	//cout << typeid(d).name() << endl;
 
	2.auto关键字经常和范围for一起使用，用来遍历数组。
	普通的遍历数组
	//int arr[] = { 0,1,2,3,4,5,6 };
	//for (int i = 0; i < sizeof(arr) / sizeof(arr[0]); ++i)
	//	cout << arr[i] << " ";
	//cout << endl;
	范围for:自动迭代，自动结束
	依次取arr中的元素，赋值给变量i（注意i是arr中元素的拷贝）
	//for (auto i : arr)
	//	cout << i << ' ';
	//cout << endl;
 
	//注意： auto* a 是在强调a是指针类型，强调a只能接收指针类型。
	/*int i = 0;
	int* ip = &i;
	auto a = i;
	///auto* aa = i; //auto* 只能接收指针类型
	auto* aa = ip;
	auto b = ip;
	cout << typeid(aa).name() << endl;
	cout << typeid(b).name() << endl;*/
 
	//3.auto结合引用和范围for一起使用，用来修改数组。
	int arr[] = { 1, 2, 3, 4, 5, 6 };
	for (auto a1 : arr)
	{
		cout << a1 << ' ';
	}
	cout << endl;
	for (auto& i : arr)
	{
		++i;
	}
	for (auto a2 : arr)
	{
		cout << a2 << ' ';
	}
	cout << endl;
 
	//注意：使用auto声明变量必须初始化
	//auto a;
	return 0;
}
 
//6.范围for的范围必须是确定的。
//void test(int a[])
//{
//	for (auto i : a)
//	{
//		cout << i << endl;
//	}
//}
~~~