
# 二维数组
```cpp
vector<vector<int>> table(size1, vector<int>(size2, 0));
```

 **_代码说明：声明一个名为 table 的容器，其元素为 vector的容器。简单来说类似一个int型的二维数组。_**

**这样，就得到了一个如下图所示的二维容器。
**![[Pasted image 20241110205915.png]]
要包含头文件#include<vector>
~~~c
    // 默认构造函数，创建一个空的 vector
    vector<int> v1; 
    
    // 创建一个包含 4 个默认初始化元素（值为 0）的 vector
    vector<int> v2(4); 
    
    // 创建一个包含 4 个元素，每个元素初始化为 10 的 vector
    vector<int> v3(4, 10); 
    
    // 使用迭代器范围（v3 的起始和结束迭代器）初始化 vector，v4 将包含 v3 的所有元素
    vector<int> v4(v3.begin(), v3.end());
    
    // 拷贝构造函数，创建一个 v2 的副本
    vector<int> v5(v2); 
    
    // 使用初始化列表创建 vector，v6 将包含 1, 2, 3, 4, 5, 6, 7 这些元素
    vector<int> v6 = {1, 2, 3, 4, 5, 6, 7}; 

    // 使用 std::string 初始化
    string s1("12345"); // 创建一个包含 "12345" 的字符串 s1
    // 使用 std::string 的迭代器初始化 std::vector<int>
    // 这里每个 char 会隐式转换为其对应的 int（ASCII 值）
    vector<int> v3(s1.begin(), s1.end()); // 使用字符串的迭代器初始化 vector<int>
    ~~~
