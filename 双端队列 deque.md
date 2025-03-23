# 双端队列
双端队列最适合的是频繁的元素的插入和删除,对于遍历没有vector容器的好

相对于队列的不同：双端数组，可以对头端进行插入删除操作，和随机访问（遍历），不同位置的插入和删除，排序操作

## deque与vector区别：

vector对于头部的插入删除效率低，数据量越大，效率越低

这是因为vector每次头部的插入都会将元素后移一位，每次操作都是O(N)的时间

deque相对而言，对头部的插入删除速度回比vector快

这是因为vector内部是一片连续的空间访问速度快

而deque内部由中控器来维护，中控器存放的是每个缓冲区的地址，所以看起来是个连续的空间，其实每次你访问的都是缓冲区的地址，再根据地址寻找对应缓冲区的值

vector访问元素时的速度会比deque快,这和两者内部实现有关

## deque的构造函数
deque<T> deqT; //默认构造形式

deque(beg, end); //构造函数将[beg, end)区间中的元素拷贝给本身。

deque(n, elem); //构造函数将n个elem拷贝给本身。

deque(const deque &deq); //拷贝构造函数
~~~
#include <deque>
//通过迭代器循环遍历
void printDeque(const deque<int>& d) 
{
	for (deque<int>::const_iterator it = d.begin(); it != d.end(); it++) {
		cout << *it << " ";
 
	}
	cout << endl;
}
 
int main() {
 
    deque<int> d1; //无参构造函数
	for (int i = 0; i < 10; i++)
	{
		d1.push_back(i);
	}
	printDeque(d1);
	deque<int> d2(d1.begin(),d1.end());
	printDeque(d2);
 
	deque<int>d3(10,100);
	printDeque(d3);
 
	deque<int>d4 = d3;
	printDeque(d4);
	return 0;
}

~~~
## deque的大小操作
deque.empty(); //判断容器是否为空

deque.size(); //返回容器中元素的个数

deque.resize(num); //重新指定容器的长度为num,若容器变长，则以默认值填充新位置。

//如果容器变短，则末尾超出容器长度的元素被删除。

deque.resize(num, elem); //重新指定容器的长度为num,若容器变长，则以elem值填充新位置。//如果容器变短，则末尾超出容器长度的元素被删除。
~~~
#include <deque>
 
void printDeque(const deque<int>& d) 
{
	for (deque<int>::const_iterator it = d.begin(); it != d.end(); it++) {
		cout << *it << " ";
 
	}
	cout << endl;
}
 
int main() {
 
	deque<int> d1;
	for (int i = 0; i < 10; i++)
	{
		d1.push_back(i);
	}
	printDeque(d1);
 
	//判断容器是否为空
	if (d1.empty()) {
		cout << "d1为空!" << endl;
	}
	else {
		cout << "d1不为空!" << endl;
		//统计大小
		cout << "d1的大小为：" << d1.size() << endl;
	}
 
	//重新指定大小
	d1.resize(15, 1);
	printDeque(d1);
 
	d1.resize(5);
	printDeque(d1);
 
	return 0;
}
~~~

## deque的插入和删除
### 两端插入操作：

push_back(elem); //在容器尾部添加一个数据

push_front(elem); //在容器头部插入一个数据

pop_back(); //删除容器最后一个数据

pop_front(); //删除容器第一个数据

### 指定位置插入：

insert(pos,elem); //在pos位置插入一个elem元素的拷贝，返回新数据的位置。

insert(pos,n,elem); //在pos位置插入n个elem数据，无返回值。

insert(pos,beg,end); //在pos位置插入[beg,end)区间的数据，无返回值。、

### 指定位置删除：

clear(); //清空容器的所有数据

erase(beg,end); //删除[beg,end)区间的数据，返回下一个数据的位置。

erase(pos); //删除pos位置的数据，返回下一个数据的位置。
~~~
#include <deque>
 
void printDeque(const deque<int>& d) 
{
	for (deque<int>::const_iterator it = d.begin(); it != d.end(); it++) {
		cout << *it << " ";
 
	}
	cout << endl;
}
//两端操作
void test01()
{
	deque<int> d;
	//尾插
	d.push_back(10);
	d.push_back(20);
	//头插
	d.push_front(100);
	d.push_front(200);
 
	printDeque(d);
 
	//尾删
	d.pop_back();
	//头删
	d.pop_front();
	printDeque(d);
}
 
//插入
void test02()
{
	deque<int> d;
	d.push_back(10);
	d.push_back(20);
	d.push_front(100);
	d.push_front(200);
	printDeque(d);
 
	d.insert(d.begin(), 1000);
	printDeque(d);
 
	d.insert(d.begin(), 2,10000);
	printDeque(d);
 
	deque<int>d2;
	d2.push_back(1);
	d2.push_back(2);
	d2.push_back(3);
 
	d.insert(d.begin(), d2.begin(), d2.end());
	printDeque(d);
 
}
 
//删除
void test03()
{
	deque<int> d;
	d.push_back(10);
	d.push_back(20);
	d.push_front(100);
	d.push_front(200);
	printDeque(d);
 
	d.erase(d.begin());
	printDeque(d);
 
	d.erase(d.begin(), d.end());
	d.clear();
	printDeque(d);
}
 
int main() {
 
	//test01();
 
	//test02();
 
    test03();
    
 
	return 0;
}
~~~
## deque的排序
依然可以用sort方法对双端队列进行排序sort(迭代的起始位置,迭代的终止位置,自定义比较函数)
