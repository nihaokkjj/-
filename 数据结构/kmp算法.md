### 前缀和后缀概念
对 p = “abcab”

p   	a	b	c	a	b
下标	1	2	3	4	5
next[ ]	0	0	0	1	2
对next[ 1 ] ：前缀 = 空集—————后缀 = 空集—————next[ 1 ] = 0;

对next[ 2 ] ：前缀 = { a }—————后缀 = { b }—————next[ 2 ] = 0;

对next[ 3 ] ：前缀 = { a , ab }—————后缀 = { c , bc}—————next[ 3 ] = 0;

对next[ 4 ] ：前缀 = { a , ab , abc }—————后缀 = { a . ca , bca }—————next[ 4 ] = 1;

对next[ 5 ] ：前缀 = { a , ab , abc , abca }————后缀 = { b , ab , cab , bcab}————next[ 5 ] = 2;

### 求next[]数组
以要找的小字符串为模板自身对照
找到相同的前后缀就匹配
未找到就把可以移动的字符串向后移，知道找到匹配的字符串 或者 直接移动到头位置
![[Pasted image 20241118100853.png]]
**代码**
~~~
for(int i = 2, j = 0; i <= m; i++)
{
    while(j && p[i] != p[j+1]) j = next[j];

    if(p[i] == p[j+1]) j++;

    next[i] = j;
}
~~~

### kmp匹配阶段
最后阶段与求next数组阶段很像
最重要的一点
**模板连永远不向后退**
都是利用之前遍历的已知信息来回退要寻找的字符串，从而节省时间
~~~
#include <iostream>

using namespace std;

const int N = 100010, M = 10010; //N为模式串长度，M匹配串长度

int n, m;
int ne[M]; //next[]数组，避免和头文件next冲突
char s[N], p[M];  //s为模式串， p为匹配串

int main()
{
    cin >> n >> s+1 >> m >> p+1;  //下标从1开始

    //求next[]数组
    for(int i = 2, j = 0; i <= m; i++)
    {
        while(j && p[i] != p[j+1]) j = ne[j];
        if(p[i] == p[j+1]) j++;
        ne[i] = j;
    }
    //匹配操作
    for(int i = 1, j = 0; i <= n; i++)
    {
        while(j && s[i] != p[j+1]) j = ne[j];
        if(s[i] == p[j+1]) j++;
        if(j == m)  //满足匹配条件，打印开头下标, 从0开始
        {
            //匹配完成后的具体操作
            //如：输出以0开始的匹配子串的首字母下标
            //printf("%d ", i - m); (若从1开始，加1)
            j = ne[j];            //再次继续匹配
        }
    }

    return 0;
}
~~~