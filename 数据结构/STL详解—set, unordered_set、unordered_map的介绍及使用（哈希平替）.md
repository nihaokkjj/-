# 文章目录
unordered系列关联式容器
unordered_set的介绍
unordered_set的使用
unordered_set的定义方式
unordered_set接口的使用
unordered_multiset
unordered_map的介绍
unordered_map的使用
unordered_map的定义方式
unordered_map接口的使用
unordered_multimap
# unordered系列关联式容器
在C++98中，STL提供了底层为红黑树结构的一系列关联式容器，在查询时的效率可达到O ( l o g N ) O(logN)O(logN)，即最差情况下需要比较红黑树的高度次，当树中的结点非常多时，查询效率也不理想。最好的查询是，进行很少的比较次数就能够将元素找到，因此在C++11中，STL又提供了4个unordered系列的关联式容器，这四个容器与红黑树结构的关联式容器使用方式基本类似，只是其底层结构不同。

## unordered_set的介绍
unordered_set是不按特定顺序存储键值的关联式容器，其允许通过键值快速的索引到对应的元素。
在unordered_set中，元素的值同时也是唯一地标识它的key。
在内部，unordered_set中的元素没有按照任何特定的顺序排序，为了能在常数范围内找到指定的key，unordered_set将相同哈希值的键值放在相同的桶中。
unordered_set容器通过key访问单个元素要比set快，但它通常在遍历元素子集的范围迭代方面效率较低。
它的迭代器至少是前向迭代器。
unordered_set的使用
### unordered_set的定义方式
方式一： 构造一个某类型的空容器。

unordered_set<int> us1; //构造int类型的空容器

方式二： 拷贝构造某同类型容器的复制品。

unordered_set<int> us2(us1); //拷贝构造同类型容器us1的复制品

方式三： 使用迭代器拷贝构造某一段内容。

string str("abcedf");
unordered_set<char> us3(str.begin(), str.end()); //构造string对象某段区间的复制品
unordered_set接口的使用
unordered_set当中常用的成员函数如下：

### 成员函数	功能
insert	插入指定元素
erase	删除指定元素
find	查找指定元素
size	获取容器中元素的个数
empty	判断容器是否为空
clear	清空容器
swap	交换两个容器中的数据
count	获取容器中指定元素值的元素个数
unordered_set当中迭代器相关函数如下：

成员函数	功能
begin	获取容器中第一个元素的正向迭代器
end	获取容器中最后一个元素下一个位置的正向迭代器
使用示例：
~~~
#include <iostream>
#include <unordered_set>
using namespace std;

int main()
{
	unordered_set<int> us;
	//插入元素（去重）
	us.insert(1);
	us.insert(4);
	us.insert(3);
	us.insert(3);
	us.insert(2);
	us.insert(2);
	us.insert(3);
	//遍历容器方式一（范围for）
	for (auto e : us)
	{
		cout << e << " ";
	}
	cout << endl; //1 4 3 2
	//删除元素方式一
	us.erase(3);
	//删除元素方式二
	unordered_set<int>::iterator pos = us.find(1); //查找值为1的元素
	if (pos != us.end())
	{
		us.erase(pos);
	}
	//遍历容器方式二（迭代器遍历）
	unordered_set<int>::iterator it = us.begin();
	while (it != us.end())
	{
		cout << *it << " ";
		it++;
	}
	cout << endl; //4 2
	//容器中值为2的元素个数
	cout << us.count(2) << endl; //1
	//容器大小
	cout << us.size() << endl; //2
	//清空容器
	us.clear();
	//容器判空
	cout << us.empty() << endl; //1
	//交换两个容器的数据
	unordered_set<int> tmp{ 11, 22, 33, 44 };
	us.swap(tmp);
	for (auto e : us)
	{
		cout << e << " ";
	}
	cout << endl; //11 22 33 44
	return 0;
}
~~~

## unordered_multiset
unordered_multiset容器与unordered_set容器的底层数据结构是一样的，都是哈希表，其次，它们所提供的成员函数的接口都是基本一致的，这里就不再列举了，这两种容器唯一的区别就是，unordered_multiset容器允许键值冗余，**即unordered_multiset容器当中存储的元素是可以重复的。**
~~~
#include <iostream>
#include <unordered_set>
using namespace std;

int main()
{
	unordered_multiset<int> ums;
	//插入元素（允许重复）
	ums.insert(1);
	ums.insert(4);
	ums.insert(3);
	ums.insert(3);
	ums.insert(2);
	ums.insert(2);
	ums.insert(3);
	for (auto e : ums)
	{
		cout << e << " ";
	}
	cout << endl; //1 4 3 3 3 2 2
	return 0;
}
~~~
由于unordered_multiset容器允许键值冗余，因此该容器中成员函数find和count的意义与unordered_set容器中的也有所不同：

**成员函数find	功能**
unordered_set容器	返回键值为val的元素的迭代器
unordered_multiset容器	返回底层哈希表中第一个找到的键值为val的元素的迭代器
**成员函数count	功能**
unordered_set容器	键值为val的元素存在则返回1，不存在则返回0（find成员函数可替代）
unordered_multiset容器	返回键值为val的元素个数（find成员函数不可替代）

# unordered_map的介绍
unordered_map是存储<key, value>键值对的关联式容器，其允许通过key值快速的索引到与其对应是value。
在unordered_map中，键值通常用于唯一地标识元素，而映射值是一个对象，其内容与此键关联。键和映射值的类型可能不同。
在内部，unordered_map**没有对<key, value>按照任何特定的顺序排序**，为了能在常数范围内找到key所对应的value，unordered_map将相同哈希值的键值对放在相同的桶中。
unordered_map容器通过key访问单个元素要比map快，但它通常在遍历元素子集的范围迭代方面效率较低。
unordered_map实现了直接访问操作符（operator[]），它允许使用key作为参数直接访问value。
它的迭代器至少是前向迭代器。

## unordered_map的使用
## unordered_map的定义方式
方式一： 指定key和value的类型构造一个空容器。

unordered_map<int, double> um1; //构造一个key为int类型，value为double类型的空容器

方式二： 拷贝构造某同类型容器的复制品。

unordered_map<int, double> um2(um1); //拷贝构造同类型容器um1的复制品

方式三： 使用迭代器拷贝构造某一段内容。

unordered_map<int, double> um3(um2.begin(), um2.end()); //使用迭代器拷贝构造um2容器某段区间的复制品

unordered_map接口的使用
## unordered_map当中常用的成员函数如下：

成员函数	功能
insert	插入键值对
erase	删除指定key值的键值对
find	查找指定key值的键值对
size	获取容器中元素的个数
empty	判断容器是否为空
clear	清空容器
swap	交换两个容器中的数据
count	获取容器中指定key值的元素个数
除了上述的成员函数之外，unordered_map容器当中还实现了[ ]运算符重载函数，该重载函数的功能非常强大：[key]

若当前容器中已有键值为key的键值对，则返回该键值对value的引用。
若当前容器中没有键值为key的键值对，则先插入键值对<key, value()>，然后再返回该键值对中value的引用。
unordered_map当中迭代器相关函数如下：

成员函数	功能
begin	获取容器中第一个元素的正向迭代器
end	获取容器中最后一个元素下一个位置的正向迭代器
使用示例：
~~~
#include <iostream>
#include <string>
#include <unordered_map>
using namespace std;

int main()
{
	unordered_map<int, string> um;
	//插入键值对方式一：构造匿名对象插入
	um.insert(pair<int, string>(1, "one"));
	um.insert(pair<int, string>(2, "two"));
	um.insert(pair<int, string>(3, "three"));
	//遍历方式一：范围for
	for (auto e : um)
	{
		cout << e.first << "->" << e.second << " ";
	}
	cout << endl; //1->one 2->two 3->three
	//插入键值对方式二：调用make_pair函数模板插入
	um.insert(make_pair(4, "four"));
	um.insert(make_pair(5, "five"));
	um.insert(make_pair(6, "six"));
	//遍历方式二：迭代器遍历
	unordered_map<int, string>::iterator it = um.begin();
	while (it != um.end())
	{
		cout << it->first << "->" << it->second << " ";
		it++;
	}
	cout << endl; //1->one 2->two 3->three 4->four 5->five 6->six
	//插入键值对方式三：利用[]运算符重载函数进行插入（常用）
	um[7] = "seven";
	um[8] = "eight";
	um[9] = "nine";
	for (auto e : um)
	{
		cout << e.first << "->" << e.second << " ";
	}
	cout << endl; //9->nine 1->one 2->two 3->three 4->four 5->five 6->six 7->seven 8->eight
	//删除键值对方式一：根据key值删除
	um.erase(5);
	//删除键值对方式二：根据迭代器删除
	unordered_map<int, string>::iterator pos = um.find(7); //查找键值为7的键值对
	if (pos != um.end())
	{
		um.erase(pos);
	}
	for (auto e : um)
	{
		cout << e.first << "->" << e.second << " ";
	}
	cout << endl; //9->nine 1->one 2->two 3->three 4->four 6->six 8->eight
	//修改键值对方式一：通过find获得迭代器，通过迭代器修改
	pos = um.find(1);
	if (pos != um.end())
	{
		pos->second = "one/first";
	}
	//修改键值对方式二：利用[]运算符重载函数进行修改（常用）
	um[2] = "two/second";
	for (auto e : um)
	{
		cout << e.first << "->" << e.second << " ";
	}
	cout << endl; //9->nine 1->one/first 2->two/second 3->three 4->four 6->six 8->eight
	//容器中key值为3的键值对的个数
	cout << um.count(3) << endl;
	//容器的大小
	cout << um.size() << endl;
	//清空容器
	um.clear();
	//容器判空
	cout << um.empty() << endl;
	//交换两个容器的数据
	unordered_map<int, string> tmp{ { 2021, "before" }, { 2022, "now" } };
	um.swap(tmp);
	for (auto e : um)
	{
		cout << e.first << "->" << e.second << " ";
	}
	cout << endl; //2021->before 2022->now
	return 0;
}
~~~

# unordered_multimap
unordered_multimap容器与unordered_map容器的底层数据结构是一样的，都是哈希表，其次，它们所提供的成员函数的接口都是基本一致的，这里就不再列举了，这两种容器唯一的区别就是，**unordered_multimap容器允许键值冗余，即unordered_multimap容器当中存储的键值对的key值是可以重复的。**
~~~
#include <iostream>
#include <string>
#include <unordered_map>
using namespace std;

int main()
{
	unordered_multimap<int, string> umm;
	//插入键值对（允许键值重复）
	umm.insert(make_pair(2022, "吃饭"));
	umm.insert(make_pair(2022, "睡觉"));
	umm.insert(make_pair(2022, "敲代码"));
	for (auto e : umm)
	{
		cout << e.first << "->" << e.second << " ";
	}
	cout << endl; //2022->吃饭 2022->睡觉 2022->敲代码
	return 0;
}
~~~

由于unordered_multimap容器允许键值对的键值冗余，因此该容器中成员函数find和count的意义与unordered_map容器中的也有所不同：

成员函数find	功能
unordered_map容器	返回键值为key的键值对的迭代器
unordered_multimap容器	返回底层哈希表中第一个找到的键值为key的键值对的迭代器
成员函数count	功能
unordered_map容器	键值为key的键值对存在则返回1，不存在则返回0（find成员函数可替代）
unordered_multimap容器	返回键值为key的键值对的个数（find成员函数不可替代）
其次，由于unordered_multimap容器允许键值对的键值冗余，调用[ ]运算符重载函数时，应该返回键值为key的哪一个键值对的value的引用存在歧义，因此在unordered_multimap容器当中没有实现[ ]运算符重载函
—

# set
将原本无序的元素插入 set 集合，**set 内部的元素自动递增排序，且去除了重复元素**。

## set 的常用函数

- **find()：**find(value) **返回 set 中 value 所对应的迭代器**，即 value 的指针（地址），如果没找到则返回 end()
- 
- - **erase()：可以删除单个元素或删除一个区间内的所有元素**
- 1. st.erase(it)，其中 it 为所需要删除元素的迭代器。时间复杂度为 O(1)，可以结合 find() 函数来使用。
2. st.erase(value)，其中 value 为所需要删除元素的值。时间复杂度为 O(logN)，N 为 set 内的元素个数。
删除一个区间内的所有元素：

st.erase(iteratorBegin, iteratorEnd)，其中 iteratorBegin 为所需要删除区间的起始迭代器， iteratorEnd 为所需要删除区间的结束迭代器的下一个地址，即取 [iteratorBegin, iteratorEnd)

equal_range()：返回一对迭代器，分别表示第一个大于或等于给定关键值的元素和第一个大于给定关键值的元素。这个返回值是一个 pair 类型，第一个是键的 lower_bound，第二个是键的 upper_bound。如果这一对定位器中哪个返回失败，则返回 end() 
```
    #include <iostream>
    #include <set>
    using namespace std;
 
    int main()
    {
        set<int> s;
        set<int>::iterator it;
        for (int i = 1 ; i <= 5; ++i)
        {
            s.insert(i);
        }
        for (it = s.begin() ; it != s.end() ; ++it)
        {
            cout << *it << " ";
        }
        cout << endl;
        pair<set<int>::const_iterator, set<int>::const_iterator> pr;
        pr = s.equal_range(3);
        cout << "第一个大于等于3的数是："<< *pr.first << endl;
        cout << "第一个大于3的数是："<< *pr.second <<endl;
        return 0;
    }

    // 输出结果
    1 2 3 4 5
    第一个大于等于3的数是：3
    第一个大于3的数是：4
```

其他方法：
```
    begin();            // 返回指向第一个元素的迭代器
    end();              // 返回指向最后一个元素的后一个位置的迭代器
    clear();            // 清除所有元素
    count();            // 返回某个值元素的个数，用于判断set中是否有该元素
    size();             // 返回集合中元素的数目
    empty();            // 如果集合为空，返回true，否则返回false
    equal_range();      // 返回集合中与给定值相等的上下限的两个迭代器
    insert();           // 在集合中插入元素 
    erase();            // 删除集合中的元素
    find();             // 返回一个指向被查找到元素的迭代器
    get_allocator();    // 返回集合的分配器
    upper_bound();      // 返回大于某个值元素的迭代器
    lower_bound();      // 返回指向大于（或等于）某值的第一个元素的迭代器
    key_comp();         // 返回一个用于元素键值比较的函数
    value_comp();       // 返回一个用于比较元素间的值的函数
    max_size();         // 返回集合能容纳的元素的最大限值
    rbegin();           // 返回set反转后的开始指针(即原来的end-1)
    rend();             // 返回set反转后的结束指针(即原来的begin-1)
    swap();             // 交换两个集合变量
    ```