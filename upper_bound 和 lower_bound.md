头函数 algorithm
## **升序函数中**
基础用法
~~~
upper_bound(begin, end, value)

在从小到大的排好序的数组中，在数组的[begin, end) 区间中二分查找第一个大于value的数，找到返回该数字的地址，没找到则返回end。

lower_bound(begin, end, value)
在从小到大的排好序的数组中，在数组的 [begin, end) 区间中二分查找第一个大于等于value的数，找到返回该数字的地址，没找到则返回end。
~~~
 ## **降序函数中**
 ~~~
 用greater<type>()重载
upper_bound(begin, end, value, greater<int>())

在从大到小的排好序的数组中，在数组的 [begin, end) 区间中二分查找第一个小于value的数，找到返回该数字的地址，没找到则返回end。

lower_bound(begin, end, value, greater<int>())

在从大到小的排好序的数组中，在数组的 [begin, end) 区间中二分查找第一个小于等于value的数，找到返回该数字的地址，没找到则返回end。
~~~
## 进阶
~~~
upper_bound(begin, end, value, cmp)
bool cmp(value, element)
~~~

eg : 找到第一个小于20的数

~~~
// 自定义函数  
// 目的是 找出 大于等于 val 的元素
bool cmp(const int& e, const int& val)
{
	return e >= val;
}
 
 
int main()
{
 
	// 有序数组---从大到小
	vector<int> v = { 30,28,26,25,21,20,19,16,1 };
 
	// lower_bound 的目的：找出第一个 false 自定义函数的值---即 第 1 个 < 20 的元素
	vector<int>::iterator it = lower_bound(v.begin(), v.end(), 20, cmp);
	if (it == v.end())
		cout << "未找到满足条件的元素" << endl;
	else
	{
		cout << *it << endl;     // 找到的元素为：19
		cout << it - v.begin() << endl;  // 下标为：6
	}
	   
	return 0;
}
~~~




