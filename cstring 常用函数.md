[Open: Pasted image 20250324084057.png](c++%E5%9F%BA%E7%A1%80/_resources/cstring%20%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0/dd44ff8c4debe0870ab4fc377fa65e01_MD5.jpeg)
![](c++%E5%9F%BA%E7%A1%80/_resources/cstring%20%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0/dd44ff8c4debe0870ab4fc377fa65e01_MD5.jpeg)

[Open: Pasted image 20250324084121.png

](c++%E5%9F%BA%E7%A1%80/_resources/cstring%20%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0/99bd14847a7de7b040db5d4dc1a72618_MD5.jpeg)
![](c++%E5%9F%BA%E7%A1%80/_resources/cstring%20%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0/99bd14847a7de7b040db5d4dc1a72618_MD5.jpeg)

# to_string
## 数字转字符串

```
int n = 114514;
string a = to_string(n);
```
## 字符串转数字
~~~
string a = "114514";
int n = atoi(a.c_str());//从第一位开始，遇到非数字停止，诺第一位不是数字则为0
~~~

# memset
~~~

//char[]型字符串
char arr[100];
memset(arr,'a',sizeof arr);//可以初始化为任意字符
for (int i = 0;i < 100;i++) cout << arr[i];
~~~
~~~
//非字符型数组
int arr[100];//按字节初始化，int为4字节
memset(arr, -1, sizeof arr);//初始化为-1或0或0x3f
//-1 = (1111 1111 1111 1111) = -1
//0  = (0000 0000 0000 0000) = 0
//0x3f=(3f 3f 3f 3f) = 0x3f3f3f3f
for (int i = 0;i < 100;i++) cout << arr[i];
————————————————
~~~

# find查找
rfind则为逆向查找，从字符串后面往前查找

当find函数未找到要查找的子字符串时，它将返回常量值string::npos 通常定义为-1；或一个很大的无符号整数类型的值

//查找目标字符串的下标
~~~
#include<iostream>
#include<string>
using namespace std;
int main() {
	string arr = "komeijikoishi";
    
    string target = "oi";
	int index = arr.find(target);//返回第一次出现目标字符串的位置
    if(arr.find(target == -1)) cout << "不存在子串" << endl;
	cout << index << endl;
    
	int index2 = arr.find("i", 5);	//从下标为5的位置开始查找
	cout << index2 << endl;

    
	int index3 = arr.find_first_of("i");	//查找目标字符串第一次出现的位置
	cout << index3 << endl;
	int index4 = arr.find_last_of("i");		//查找目标字符串最后一次出现的位置
	cout << index4 << endl;

	return 0;
}
~~~
————————————————

# compare
比较字典序

区分大小写，从头开始依次比较字符对应ASCII码大小
~~~
string A = "12345";
string B = "12454";
cout << A.compare(B);
//A>B 返回1；	A<B 返回-1;	A==B 返回0；


//str_cmp比较char类型字符串的字典序
char A[] = "abc";
char B[] = "abc";
strcmp(A,B)
//A>B 返回1；	A<B 返回-1;	A==B 返回0；
————————————————
~~~

# replace
字符替换
~~~
//a.replace(pos,len,"str");  从pos位置开始，长度为len，替换为str
string a = "abcdefg";
a.replace(0, 4, "66");//或者用迭代器a.replace(a.begin(), a.begin() + 4, "66");
//replace(a.begin(),a.end(),'a','*');
cout << a;//66efg

//a.replace(pos,len,n,'c');	从pos位置开始，长度为len,替换为重复n次的字符c
string a = "abcdefg";
a.replace(0,4,3,'6');

//将字符串中的a用b替换
replace(str.begin(), str.end(), 'a', 'b');  //需包含#include <algorithm> 
————————————————
~~~

# algorithm

[Open: Pasted image 20250324084847.png](c++%E5%9F%BA%E7%A1%80/_resources/cstring%20%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0/53a4ca83f5258633a1c1371f4157a1f7_MD5.jpeg)
![](c++%E5%9F%BA%E7%A1%80/_resources/cstring%20%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0/53a4ca83f5258633a1c1371f4157a1f7_MD5.jpeg)

## count_if
count_if
返回满足条件范围内的元素个数
~~~
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
vector <int> myvector;
bool isEven(int elem){ return elem % 2 == 0;}
bool cmp(int elem) { return elem > 2; }
void main(){
	for (int i = 0;i < 9;i++){
		myvector.push_back(i+1);
		cout << myvector[i];
	}
	// 计算偶数个数
	int ctif = count_if(myvector.begin(), myvector.end(), isEven);
	// 计算大于2的个数
	int ctg = count_if(myvector.begin(), myvector.end(), cmp);
	cout << "偶数元素个数:" << ctif << endl;
	cout << "超过2的元素个数: " << ctg << endl;
}
