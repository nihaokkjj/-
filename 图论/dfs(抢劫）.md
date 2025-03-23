# 第一种方法
用记忆数组记录已经递推过的分支，若mem【u】已经存在，则直接返回
从第一个房子开始，
因为不能同时抢劫相邻的房子
所以要么抢劫现在所在的这个房子，不枪下一个
要么不抢现在所在的房子，抢劫下一个
![[Pasted image 20241204123411.png]] # 第二种方法
## 倒着抢劫
~~~
#include<bits/stdc++.h>  
using namespace std;  
const int N = 101;  
int f[N], home[N];  
int main()  
{  
    int n;  
    scanf ("%d", &n);  
    for (int i = 1; i <= n; ++i) scanf ("%d", &home[i]);  
  
    for (int i = n; i >= 1; --i)  
    {  
        f[i] = max(f[i + 1], f[i + 2] + home[i]);  
    }  
    printf ("%d", f[1]);  
    return 0;  
}
~~~
## 正着抢劫
~~~
#include<bits/stdc++.h>  
using namespace std;  
const int N = 101;  
int f[N], home[N];  
int main()  
{  
    int n;  
    scanf ("%d", &n);  
    for (int i = 1; i <= n; ++i) scanf ("%d", &home[i]);  
  
    for (int i = 1; i <= n; ++i)  
    {  
        f[i + 2] = max(f[i + 1], f[i] + home[i]);  
        //本来是f[i] = max(f[i - 1], f[i - 2] + home[i]),
        //若这样写，会导致当f[i - 2]数组越界，将i加上2来映射，就解决了这个问题
    }  
    printf ("%d", f[ n + 2]);  
    return 0;  
}
~~~
# 第三种（优化空间的方法）
~~~
  
 //Created by sai_8 on 2024/12/4.  
  
#include<bits/stdc++.h>  
using namespace std;  
const int N = 101;  
int tmp1, tmp2, newf, f[N], home[N];  
int main()  
{  
    int n;  
    scanf ("%d", &n);  
    for (int i = 1; i <= n; ++i) scanf ("%d", &home[i]);  
  
    for (int i = n; i >= 1; --i)  
    {  
        newf = max (tmp1, tmp2 + home[i]);  
        //现在顺序 tmp2  tmp1  newf
        //tmp2代表现在所在房子的前两个
        tmp2 = tmp1;  //将数组向左移
        tmp1 = newf;  
    }  
    printf ("%d", newf);  
    return 0;  
}
~~~