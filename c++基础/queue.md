### 不能用[vector](https://so.csdn.net/so/search?q=vector&spm=1001.2101.3001.7020 "vector")容器初始化queue

因为queue转换器要求容器支持front()、back()、push_back()及 pop_front()，说明queue的数据从容器后端入栈而从前端出栈。所以可以使用[deque](https://so.csdn.net/so/search?q=deque&spm=1001.2101.3001.7020)（double-ended queue，双端队列）和list对queue初始化，而vector因其缺少pop_front（），不能用于queue。

## 二、queue常用[函数](https://marketing.csdn.net/p/3127db09a98e0723b83b2914d9256174?pId=2782&utm_source=glcblog&spm=1001.2101.3001.7020)

### 1.常用函数

1. push() 在队尾插入一个元素
2. pop() 删除队列第一个元素
3. size() 返回队列中元素个数
4. empty() 如果队列空则返回true
5. front() 返回队列中的第一个元素
6. back() 返回队列中最后一个元素

### 2.函数运用示例

1：**push（）在队尾插入一个元素**

```cpp
queue <string> q;q.push("first");q.push("second");cout<<q.front()<<endl;
```

输出 first

2：**pop() 将队列中最靠前位置的元素删除，没有返回值**

```cpp
queue <string> q;q.push("first");q.push("second");q.pop();cout<<q.front()<<endl;
```

输出 second 因为 first 已经被pop（）函数删掉了

3：**size() 返回队列中元素个数**

```cpp
queue <string> q;q.push("first");q.push("second");cout<<q.size()<<endl;
```

输出2，因为队列中有两个元素

4：**empty() 如果队列空则返回true**

```cpp
queue <string> q;cout<<q.empty()<<endl;q.push("first");q.push("second");cout<<q.empty()<<endl;
```

分别输出1和0  
最开始队列为空，返回值为1（ture）；  
插入两个元素后，队列不为空，返回值为0（false）；

5：front() 返回队列中的第一个元素

```cpp
queue <string> q;q.push("first");q.push("second");cout<<q.front()<<endl;q.pop();cout<<q.front()<<endl;
```

第一行输出first；  
第二行输出second，因为pop（）已经将first删除了

6：**back() 返回队列中最后一个元素**
