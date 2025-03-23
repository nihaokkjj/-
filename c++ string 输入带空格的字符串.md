.cin.getline()或cin.get()
~~~
#include<iostream>
using namespace std;
 
#include<string>
int main()
{
	char a[10];
	cin.getline(a,5);//接收5个字符
	cout << a;
	return 0;
}
~~~
cin.getline()实际上有三个参数，cin.getline(接收字符串的变量，接收字符个数，结束字符)，当第三个参数省略时，系统会默认为'\0'

//cin.get()与cin.getline()用法一致

**区别cin.getline()和getline()**
这是两个不一样的函数，cin.getline()属于istream流，而getline()属于string流

cin.getline()不需要引头文件，getline()头文件为#include<string>
