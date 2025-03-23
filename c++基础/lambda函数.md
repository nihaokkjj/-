## **lambda表达式的语法** 

> **`lambda` 表达式** 分为以下几部分： 

- **`[ ]` 捕捉列表**
- **`( )`** **参数列表**
- **`mutable`** **关键字**
- **`->returntype`** **返回值类型**
- **`{ }`** **函数体**

```scss
lambda表达式：[ ]( ) mutable ->returntype { }
```
![[Pasted image 20241112105231.png]]
其中，( ) 参数列表、mutable、->returntype 都可以省略 

省略 ( )参数列表 表示当前是一个无参函数对象
省略 mutable关键字 表示保持捕捉列表中参数的常量属性
省略 ->returntype返回值类型 表示具体的返回值类型由函数体决定，编译器会自动推导出返回值类型
# 使用
 使用 auto 推导 匿名函数对象 的类型，然后创建 add 函数对象
 ```
int main()
{
	auto add = [](int x, int y)->int { return x + y; };
 
	int ret = add(1, 2); // 实现1 + 2
 
	cout << ret << endl;
	return 0;
}
```

***要改变外部变量必须 加&*** ； 例如：
~~~
. auto swap = [&x, &y]() ->void
~~~
***若只想改变一个变量***
~~~
auto func = [&x, y]()mutable ->void
~~~
***改变全部变量***
```
auto func = [&]()->void
```
- **全部传值捕捉** 也能一键捕捉外部变量，不过此时捕获的是外部变量的值，并非变量本身，无法对其进行修改（可以通过 **`mutable`关键字** 取消常性）
```
- auto func = [=]()->void
				{
					cout << x << " " << y << " " << z << " " << endl;
					cout << a << " " << b << " " << c << " " << endl;
					cout << str << endl;
					cout << "&str: " << &str << endl << endl;
				};

