# 一维
```
vector<数据类型> 名字
vector<T> vec          定义一个T数据类型的空vector元素，执行默认初始化，有些类型不支持默认初始化
vector<T> vec(n,val)   定义n个T数据类型的元素，每个元素的值为val
vector<T> vec(n)       定义n个T数据类型的元素，执行默认初始化，有些类型不支持默认初始化
vector<T> vec{a,b,c...}vec中每个元素被赋予相应的初始值
vector<T> vec={a,b,c...}等价于vec{a,b,c...}
vector<T> vec2(vec1)   vec2中包含有vec1所有元素的副本,把vec1中的元素拷贝给vec2
vector<T> vec2=vec1    等价于vec2(vec1),注意vec2与vec1必须具有相同的数据类型
 
```

# 二维
```
// 初始化一个 二维的matrix, 行M,列N,且值为0
vector<vector<int>> matrix(M,vector<int>(N));
//等价于下面的
vector<vector<int> > matrix(M); 
for(int i=0;i<M;i++) {
    matrix[i].resize(N);
}
//等价于下面的
vector< vector<int> > matrix;
matrix.resize(M);//M行
for(int i=0;i<matrix.size();i++){
    matrix[i].resize(N);//每一行都是N列
}
    
// 初始化一个 二维的matrix, 行M,列N,且值自定义为data;
vector<vector<int>> matrix(M,vector<int>(N,data));



```