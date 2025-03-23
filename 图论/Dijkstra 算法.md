Dijkstra
## 朴素版dijkstra适合稠密图
思路
集合S为已经确定最短路径的点集。
1. 初始化距离
一号结点的距离为零，其他结点的距离设为无穷大（看具体的题）。
2. 循环n次，每一次将集合S之外距离最短X的点加入到S中去（这里的距离最短指的是距离1号点最近。
点X的路径一定最短，基于贪心，严格证明待看）。然后用点X更新X邻接点的距离。
时间复杂度分析
寻找路径最短的点：O(n<sup>2</sup>)

加入集合S：O(n)

更新距离：O(m)

所以总的时间复杂度为O(n<sup>2</sup>)

具体问题
稠密图用邻接矩阵存。
~~~
#include<iostream>
#include<cstring>
#include<cstdio>
#include<algorithm>

using namespace std;

const int N = 510, M = 100010;

int g[N][N], dist[N];
bool visited[N];

int n, m;

int dijkstra()
{
    memset(dist, 0x3f, sizeof(dist));
    dist[1] = 0;
    for(int i = 1; i <= n; i++)
    {
        int t = -1;
        for(int j = 1; j <= n; j++)
        {
            if(!visited[j] && (t == -1 || dist[j] < dist[t]))
                t = j;
        }
        visited[t] = true;
        for(int j = 1; j <= n; j++)
            dist[j] = min(dist[j], dist[t] + g[t][j]);
    }
    if(dist[n] == 0x3f3f3f3f) return -1;
    return dist[n];
}

int main()
{
    scanf("%d%d", &n, &m);

    memset(g, 0x3f, sizeof(g));
    while (m--)
    {
        int x, y, c;
        scanf("%d%d%d", &x, &y, &c);
        g[x][y] = min(g[x][y], c);
    }
    cout << dijkstra() << endl;
    return 0;
}
~~~
## 堆优化版dijkstra适合稀疏图
思路
堆优化版的dijkstra是对朴素版dijkstra进行了优化，在朴素版dijkstra中时间复杂度最高的寻找距离
最短的点O(n<sup>2</sup>)可以使用最小堆优化。
1. 一号点的距离初始化为零，其他点初始化成无穷大。
2. 将一号点放入堆中。
3. 不断循环，直到堆空。每一次循环中执行的操作为：
    弹出堆顶（与朴素版diijkstra找到S外距离最短的点相同，并标记该点的最短路径已经确定）。
    用该点更新临界点的距离，若更新成功就加入到堆中。
时间复杂度分析
寻找路径最短的点：O(n)
加入集合S：O(n)

更新距离：O(mlogn)

具体问题
~~~
#include<iostream>
#include<cstring>
#include<queue>

using namespace std;

typedef pair<int, int> PII;

const int N = 100010; // 把N改为150010就能ac

// 稀疏图用邻接表来存
int h[N], e[N], ne[N], idx;
int w[N]; // 用来存权重
int dist[N];
bool st[N]; // 如果为true说明这个点的最短路径已经确定

int n, m;

void add(int x, int y, int c)
{
    // 有重边也不要紧，假设1->2有权重为2和3的边，再遍历到点1的时候2号点的距离会更新两次放入堆中
    // 这样堆中会有很多冗余的点，但是在弹出的时候还是会弹出最小值2+x（x为之前确定的最短路径），
    // 并标记st为true，所以下一次弹出3+x会continue不会向下执行。
    w[idx] = c;
    e[idx] = y;
    ne[idx] = h[x]; 
    h[x] = idx++;
}

int dijkstra()
{
    memset(dist, 0x3f, sizeof(dist));
    dist[1] = 0;
    priority_queue<PII, vector<PII>, greater<PII>> heap; // 定义一个小根堆
    
    // 这里heap中为什么要存pair呢，首先小根堆是根据距离来排的，所以有一个变量要是距离，
    // 其次在从堆中拿出来的时候要知道知道这个点是哪个点，不然怎么更新邻接点呢？所以第二个变量要存点。
    
    heap.push({ 0, 1 }); // 这个顺序不能倒，pair排序时是先根据first，再根据second，
                         // 这里显然要根据距离排序
    while(heap.size())
    {
        PII k = heap.top(); // 取不在集合S中距离最短的点
        heap.pop();
        int ver = k.second, distance = k.first;

        if(st[ver]) continue;
        st[ver] = true;

        for(int i = h[ver]; i != -1; i = ne[i])
        {
            int j = e[i]; // i只是个下标，e中在存的是i这个下标对应的点。
            if(dist[j] > distance + w[i])
            {
                dist[j] = distance + w[i];
                heap.push({ dist[j], j });
            }
        }
    }
    if(dist[n] == 0x3f3f3f3f) return -1;
    else return dist[n];
}

int main()
{
    memset(h, -1, sizeof(h));
    scanf("%d%d", &n, &m);

    while (m--)
    {
        int x, y, c;
        scanf("%d%d%d", &x, &y, &c);
        add(x, y, c);
    }

    cout << dijkstra() << endl;

    return 0;
}
~~~