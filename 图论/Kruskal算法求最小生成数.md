# 算法思路：

1. 将所有边按照权值的大小进行升序排序，然后从小到大一一判断。

2. 如果这个边与之前选择的所有边不会组成回路，就选择这条边分；反之，舍去。

3. 直到具有 n 个顶点的连通网筛选出来 n-1 条边为止。

4. 筛选出来的边和所有的顶点构成此连通网的最小生成树。

判断是否会产生回路的方法为：使用并查集。

1. 在初始状态下给各个个顶点在不同的集合中。、

2. 遍历过程的每条边，判断这两个顶点的是否在一个集合中。

3. 如果边上的这两个顶点在一个集合中，说明两个顶点已经连通，这条边不要。如果不在一个集合中，则要这条边。

# 举例
举个例子，下图一个连通网，克鲁斯卡尔算法查找图 1 对应的最小生成树，需要经历以下几个步骤：
![](Pasted%20image%2020241220132841.png)
![](Pasted%20image%2020241220132858.png)
![](Pasted%20image%2020241220132913.png)
```
#include <iostream>
#include <cstring>
#include <algorithm>

using namespace std;
const int N = 100010;
int p[N];//保存并查集

struct E{
    int a;
    int b;
    int w;
    bool operator < (const E& rhs){//通过边长进行排序
        return this->w < rhs.w;
    }

}edg[N * 2];
int res = 0;

int n, m;
int cnt = 0;
int find(int a){//并查集找祖宗
    if(p[a] != a) p[a] = find(p[a]);//若用return可能会不通过
    return p[a];
}
void klskr(){
    for(int i = 1; i <= m; i++)//依次尝试加入每条边
    {
        int pa = find(edg[i].a);// a 点所在的集合
        int pb = find(edg[i].b);// b 点所在的集合
        if(pa != pb){//如果 a b 不在一个集合中
            res += edg[i].w;//a b 之间这条边要
            p[pa] = pb;// 合并a b
            cnt ++; // 保留的边数量+1
        }
    }
}
int main()
{

    cin >> n >> m;
    for(int i = 1; i <= n; i++) p[i] = i;//初始化并查集
    for(int i = 1; i <= m; i++){//读入每条边
        int a, b , c;
        cin >> a >> b >>c;
        edg[i] = {a, b, c};
    }
    sort(edg + 1, edg + m + 1);//按边长排序
    klskr();
    //如果保留的边小于点数-1，则不能连通
    if(cnt < n - 1) {
        cout<< "impossible";
        return 0;
    }
    cout << res;
    return 0;
}

```