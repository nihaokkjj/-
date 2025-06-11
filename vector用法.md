### 1、vector的定义
单独定义一个vector：

vector<typename> name;
上面这个定义其实相当于是一维数组name[size]，只不过其size可以根据需要进行变化，这就是“变长数组”的名字的由来。

这里的typename可以是任何基本类型，例如int、double、char、结构体等，也可以是STL标准容器，例如set、queue、vector等。

接下来我们来看下定义二维vector数组的方法：

vector<typename> Arrayname[size];    
其中，Arrayname[]中的每一个元素都是一个vector。我们可以把二维vector数组当做两个维都可以变长的二维数组来理解。

例如：
~~~
vector<int> vi[100];
//vi[0] ~ vi[100 - 1]中每一个都是一个vector容器
# 2、vector常用初始化方法
1、使用花括号直接赋值：
vector<int> v{1,2,3,4,5}; //直接使用花括号赋值
for(auto i : v) cout << i << " "; //输出1 2 3 4 5
2、使用圆括号赋值：
vector<int> v(5); //初始化5个值为0的元素
for(auto i : v) cout << i << " "; //输出0 0 0 0 0
vector<int> v(5, 4); //初始化5个值为4的元素
for(auto i : v) cout << i << " "; //输出4 4 4 4 4
~~~
# 3、vector容器内元素的访问
1、通过下标访问：
定义为vector<int> v 的vector容器，可以使用 v[0]、v[1]、v[2]...这种方式来访问。当然，下标不能越界(v.size()-1之内)。

注：v[0]、v[1]、v[2]等价于*(v.begin() )、*(v.begin() + 1)、*(v.begin() + 2)。

2、通过迭代器来访问：
迭代器(iterator)可以理解为一种类似指针的东西，其定义是：

vector<typename>::iterator it;
这样就得到了迭代器it，并且可以通过 *it 来访问vector里的元素。

访问方式：

#include<bits/stdc++.h>
using namespace std;
int main(){
	vector<int> v;
	v.push_back(1);	//依次输入1、 2、 3 
	v.push_back(2);
	v.push_back(3);
	for(vector<int>::iterator it = v.begin(); it != v.end(); it++){
		cout << *it << " ";
	}
	
    return 0;
} 
输出结果：

1 2 3
# 4、vector常用函数实例解析
## 1、push_back():
v.push_back(x)，就是在vector容器v后面添加一个元素x，时间复杂度为O(1)。

#include<bits/stdc++.h>
using namespace std;
int main(){
	vector<int> v;
	for(int i = 1; i <= 3; i++){
		v.push_back(i);
	}
	for(vector<int>::iterator it = v.begin(); it != v.end(); it++){
		cout << *it << " ";
	}
	return 0;
} 
输出结果:

1 2 3
## 2、pop_back():
pop_back()可以删除vector的尾元素，时间复杂度为O(1)：

#include<bits/stdc++.h>
using namespace std;
int main(){
	vector<int> v;
	for(int i = 1; i <= 3; i++){
		v.push_back(i);	//将1、2、3 依次插入v的队尾 
	}
	v.pop_back();	//删除尾元素 
	for(vector<int>::iterator it = v.begin(); it != v.end(); it++){
		cout << *it << " ";
	}
	
    return 0;
} 
输出结果：

1 2
## 3、size()：
size()用来获得vector中元素的个数，时间复杂度为O(1)。size()返回的是unsigned类型：

#include<bits/stdc++.h>
using namespace std;
int main(){
	vector<int> v;
	for(int i = 1; i <= 3; i++){
		v.push_back(i);	//将1、2、3 依次插入v的队尾 
	}
	v.pop_back();	//删除尾元素 
	//for(vector<int>::iterator it = v.begin(); it != v.end(); it++){
//		cout << *it << " ";
//	}
	cout << v.size();    //获取容器长度
 
    return 0;
} 
输出结果：

2
## 4、clear()：
clear()用来清空vector中的所有元素，时间复杂度为O(N)，N为vector中的元素个数：

#include<bits/stdc++.h>
using namespace std;
int main(){
	vector<int> v;
	for(int i = 1; i <= 3; i++){
		v.push_back(i);	//将1、2、3 依次插入v的队尾 
	}
	v.pop_back();	//删除尾元素 
	v.clear();	
	//for(vector<int>::iterator it = v.begin(); it != v.end(); it++){
//		cout << *it << " ";
//	}
	cout << v.size();
	
    return 0;
} 
输出结果：

0
## 5、insert():
insert(it, x)用来向vector的任意迭代器it处插入一个元素x，时间复杂度O(N)：

#include<bits/stdc++.h>
using namespace std;
int main(){
	vector<int> v;
	for(int i = 1; i <= 5; i++){
		v.push_back(i);	//将1、2、3、4、5 依次插入v的队尾 
	}
	v.insert(v.begin() + 2, -1);	//将-1插入v[2]的位置 
	for(vector<int>::iterator it = v.begin(); it != v.end(); it++){
		cout << *it << " ";
	}
	
	return 0; 
} 
输出结果：

1 2 -1 3 4 5
 

insert(pos,first,last) 在 pos 位置之前，插入其他容器（不仅限于vector）中位于 [first,last) 区域的所有元素(简单说就是把两个容器拼接在一起)。

#include<bits/stdc++.h>
using namespace std;
 
int main(){
	vector<int> v, v1, v2;
    for(int i = 1; i <= 3; i++) v.push_back(i);
	for(int i  = 11; i <= 13; i++) v1.push_back(i);
	for(int i  = 101; i <= 103; i++) v2.push_back(i);
	v.insert(v.end(), v1.begin(), v1.end());  //输出1 2 3 11 12 13
	v.insert(v.end(), v2.begin(), v2.end()); //输出1 2 3 11 12 13 101 102 103
 
    return 0;
}
## 6、erase():
erase()有两种用法：删除单个元素、删除一个区间内所有元素。时间复杂度为O(N)。

①删除单个元素：

erase(it)即删除迭代器为it处的元素：

#include<bits/stdc++.h>
using namespace std;
int main(){
	vector<int> v;
	for(int i = 1; i <= 5; i++){
		v.push_back(i);	//将1、2、3、4、5 依次插入v的队尾 
	}
	v.erase(v.begin() + 2);	//删除3 
	for(vector<int>::iterator it = v.begin(); it != v.end(); it++){
		cout << *it << " ";
	}
	
	return 0; 
} 
输出结果：

1 2 4 5
②删除一个区间内的所有元素：

erase(first, last)即删除[first, last）内的所有元素：

#include<bits/stdc++.h>
using namespace std;
int main(){
	vector<int> v;
	for(int i = 1; i <= 5; i++){
		v.push_back(i);	//将1、2、3、4、5 依次插入v的队尾 
	}
	v.erase(v.begin() + 1, v.begin() + 3);	//删除2和3 
	for(vector<int>::iterator it = v.begin(); it != v.end(); it++){
		cout << *it << " ";
	}
	
	return 0; 
} 
输出结果：

1 4 5
如果想要用erase清空vector容器，正确的写法是 v.erase(v.begin(), v.end())，v.end() 表示的是尾元素的下一个地址。

## 7. insert
接着这个问题，顺便总结一下C++ STL的vector里insert操作常用的注意事项。
vector中的insert有三种用法：
1.在指定位置loc前插入值为val的元素,返回指向这个元素的迭代器；
2.在指定位置loc前插入num个值为val的元素；
3.在指定位置loc前插入区间[start, end)的所有元素；
iterator insert( iterator loc, const TYPE &val );
void insert( iterator loc, size_type num, const TYPE &val );
void insert( iterator loc, input_iterator start, input_iterator end );
就效率方面来说，区间成员函数应该优于与之对应的单元素成员函数。

比如，假定你要把一个int数组拷贝到一个vector的前端。使用vector的区间insert函数，非常简单：

int data[numValues]; //假定numValues在别处定义
vector<int> v;
...
v.insert(v.begin(), data, data + numValues); //把整数插入到v的前端

如果显示地调用单元素插入，则应该写成这样：

vector<int>::iterator insertLoc(v.begin());
for (int i = 0; i < numValues; i++){
	insertLoc = v.insert(insertLoc, data[i]);
	++insertLoc;
}
————————————————

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
                        
原文链接：https://blog.csdn.net/weixin_38742280/article/details/104627837