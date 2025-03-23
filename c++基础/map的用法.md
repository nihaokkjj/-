### 1、 map构造函数
默认构造函数
~~~
std::map<int, std::string> myMap; // 创建一个空的map，键类型为int，值类型为std::string
~~~
拷贝构造函数
~~~
std::map<int, std::string> myMap1 = { {1, "one"}, {2, "two"} };  
std::map<int, std::string> myMap2(myMap1); // 使用myMap1初始化myMap2，myMap2现在包含myMap1的所有元素
~~~
mp.size()返回有效元素个数

mp.count(5)判断5这个key是否存在，存在返回1，没有则返回0

mp.clear()清空mp容器

mp.empty()判断mp容器是否为空，为空返回1，不为空返回0

mp.find(3)返回key为3的迭代器，如果不存在返回mp.end()

mp.erase(4)根据4这个key去删除一对元素
### 2、 map赋值操作（=，swap）
### 重载等号操作符

std::map<int, std::string> myMap1 = { {1, "one"}, {2, "two"} };  
std::map<int, std::string> myMap2;  
myMap2 = myMap1; // 使用重载的等号操作符将myMap1的内容赋值给myMap2
1
2
3
### swap函数
~~~
std::map<int, std::string> myMap1 = { {1, "one"}, {2, "two"} };  
std::map<int, std::string> myMap2 = { {3, "three"}, {4, "four"} };  
myMap1.swap(myMap2); // 交换myMap1和myMap2的内容，现在myMap1包含{3, "three"}, {4, "four"}，myMap2包含{1, "one"}, {2, "two"}
~~~

### 3、 map的容量（size、empty）
### size函数
~~~
std::map<int, std::string> myMap = { {1, "one"}, {2, "two"}, {3, "three"} };  
std::size_t size = myMap.size(); // size现在是3，因为myMap中有3个元素
~~~
### empty函数
~~~
std::map<int, std::string> myMap;  
if (myMap.empty()) {  
    std::cout << "The map is empty." << std::endl; // 输出"The map is empty."，因为myMap是空的  
} else {  
    std::cout << "The map is not empty." << std::endl;  
}
~~~
### 二、map的增删查改
以下是针对map插入和删除操作的示例代码：

### 1、map插入数据元素操作
~~~
#include <iostream>  
#include <map>  
#include <string>  
  
int main() {  
    std::map<int, std::string> mapStu;  
  
    // 第一种 通过pair的方式插入对象  
    mapStu.insert(std::pair<int, std::string>(3, "小张"));  
  
    // 第二种 通过make_pair的方式插入对象（注意：您的示例中写成了inset，这是错误的，应该是insert）  
    mapStu.insert(std::make_pair(-1, "校长"));  
  
    // 第三种 通过value_type的方式插入对象  
    mapStu.insert(std::map<int, std::string>::value_type(1, "小李"));  
  
    // 第四种 通过数组的方式插入值  
    // 这种方式在键已存在时更新对应的值，在键不存在时插入新的键值对  
    mapStu[3] = "小刘"; // 注意：这会替换掉key为3的原始值"小张"  
    mapStu[5] = "小王";  
  
    // 输出map内容  
    for (const auto& kv : mapStu) {  
        std::cout << kv.first << ": " << kv.second << std::endl;  
    }  
  
    return 0;  
}
~~~

### 2、map键值对value的修改
map容器中，改变某个键（key）对应的值（value）可以通过以下方式实现。

使用下标操作符（operator[]）
下标操作符可以用于访问或修改map中的元素。如果键已经存在，它会返回对应的引用，你可以直接通过这个引用修改值。如果键不存在，它会创建一个新的键值对，键为你提供的键，值为该类型的默认值。
~~~
std::map<int, std::string> mapStu;  
mapStu[3] = "小张"; // 如果键3不存在，会创建一个新的键值对(3, "小张")  
mapStu[3] = "小刘"; // 如果键3已经存在，会更新其对应的值为"小刘"
~~~
### 使用find方法和迭代器
首先，使用find方法查找键在map中的位置，然后检查返回的迭代器是否指向map的结束位置（即键是否不存在）。如果键存在，可以通过迭代器访问并修改其对应的值。
~~~
std::map<int, std::string> mapStu;  
mapStu[3] = "小张";  
  
// 使用find查找键3  
auto it = mapStu.find(3);  
if (it != mapStu.end()) {  
    // 键存在，修改其对应的值  
    it->second = "小刘";  
} else {  
    // 键不存在，可以选择插入新的键值对  
    mapStu[3] = "小刘";  
}
~~~
### 3、map的删操作（erase、clear）
假设mapStu是一个map容器，则：
~~~
mapStu.clear(); //删所有
mapStu.erase(it);//删迭代器指定
mapStu.erase(beg, end);//删key区间
mapStu.erase(key1);  //删key对应
~~~

~~~
#include <iostream>  
#include <map>  
#include <string>  
  
int main() {  
    std::map<int, std::string> mapStu;  
  
    // 假设已经插入了一些元素  
    mapStu.insert(std::pair<int, std::string>(3, "小张"));  
    mapStu.insert(std::pair<int, std::string>(5, "小王"));  
    mapStu.insert(std::pair<int, std::string>(7, "小赵"));  
  
    // 删除所有元素  
    mapStu.clear();  
    std::cout << "After clear(): ";  
    for (const auto& kv : mapStu) {  
        std::cout << kv.first << ": " << kv.second << " ";  
    }  
    std::cout << std::endl;  
  
    // 重新插入一些元素  
    mapStu.insert(std::pair<int, std::string>(3, "小张"));  
    mapStu.insert(std::pair<int, std::string>(5, "小王"));  
    mapStu.insert(std::pair<int, std::string>(7, "小赵"));  
  
    // 删除指定迭代器所指的元素  
    auto it = mapStu.find(5);  
    if (it != mapStu.end()) {  
        mapStu.erase(it);  
    }  
  
    // 输出map内容  
    std::cout << "After erase(pos): ";  
    for (const auto& kv : mapStu) {  
        std::cout << kv.first << ": " << kv.second << " ";  
    }  
    std::cout << std::endl;  
  
    // 重新插入一些元素  
    mapStu.insert(std::pair<int, std::string>(3, "小张"));  
    mapStu.insert(std::pair<int, std::string>(5, "小王"));  
    mapStu.insert(std::pair<int, std::string>(7, "小赵"));  
  
    // 删除指定区间的元素  
    auto beg = mapStu.find(3);  
    auto end = mapStu.find(7);  
    mapStu.erase(beg, end); // 注意：这里删除的是[beg, end)区间  
  
    // 输出map内容  
    std::cout << "After erase(beg, end): ";  
    for (const auto& kv : mapStu) {  
        std::cout << kv.first << ": " << kv.second << " ";  
    }  
    std::cout << std::endl;  
  
    // 重新插入一些元素  
    mapStu.insert(std::pair<int, std::string>(3, "小张"));  
    mapStu.insert(std::pair<int, std::string>(5, "小王"));  
  
    // 删除指定key的元素  
    mapStu.erase(5);  
  
    // 输出map内容  
    std::cout << "After erase(keyElem): ";  
    for (const auto& kv : mapSt
————————————————

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
                        
原文链接：https://blog.csdn.net/ULTRAmanTAROACE/article/details/137115610