# 数字三角形
[Open: Pasted image 20250316144642.png](%E7%AE%97%E6%B3%95/dp/_resources/%E7%BA%BF%E6%80%A7dp/20563cea50066cbc26e0b793e7fdbe27_MD5.jpeg)
![](%E7%AE%97%E6%B3%95/dp/_resources/%E7%BA%BF%E6%80%A7dp/20563cea50066cbc26e0b793e7fdbe27_MD5.jpeg)
```
#include<bits/stdc++.h>
using namespace std;
const int N = 1e4 + 10;

int f[N][N];
int main()
{
	
	ios::sync_with_stdio(0);
	cin.tie(0);
	cout.tie(0) ;
	int n;
	cin >> n;
	
	for (int i = 1; i <= n; ++i)
	for (int j = 1; j <= i; ++j) 
	    cin >> f[i][j];
	    
	for (int i = n - 1; i >= 1; --i)
	for (int j = 1; j <= i; ++j)
	f[i][j] = max(f[i + 1][j] , f[i + 1][j + 1]) + f[i][j];
	
	cout << f[1][1];
	
	return 0;
 } 
```

# 最长上升子序列
状态表示：*f[i]表示从第一个数字开始算，以w[i]结尾的最大的上升序列。(以w[i]结尾的所有上升序列中属性为最大值的那一个)*

状态计算（集合划分）：j∈(0,1,2,..,i-1), 在w[i] > w[j]时，
f[i] = max(f[i], f[j] + 1)。
有一个边界，若前面没有比i小的，f[i]为1（自己为结尾）。

最后在找f[i]的最大值。

时间复杂度
[Open: Pasted image 20250316152129.png](%E7%AE%97%E6%B3%95/dp/_resources/%E7%BA%BF%E6%80%A7dp/15827e840274dc3a5a6c0b838ea1a19c_MD5.jpeg)
![](%E7%AE%97%E6%B3%95/dp/_resources/%E7%BA%BF%E6%80%A7dp/15827e840274dc3a5a6c0b838ea1a19c_MD5.jpeg)
~~~
#include <iostream>

using namespace std;

const int N = 1010;

int n;
int w[N], f[N];

int main() {
    cin >> n;
    for (int i = 0; i < n; i++) cin >> w[i];

    int mx = 1;    // 找出所计算的f[i]之中的最大值，边算边找
    for (int i = 0; i < n; i++) {
        f[i] = 1;    // 设f[i]默认为1，找不到前面数字小于自己的时候就为1
        for (int j = 0; j < i; j++) {
            if (w[i] > w[j]) f[i] = max(f[i], f[j] + 1);  
      // 前一个小于自己的数结尾的最大上升子序列加上自己，即+1
        }
        mx = max(mx, f[i]);
    }

    cout << mx << endl;
    return 0;
}
~~~

# 最长上升子序列II

实际上这个栈【不用于记录最终的最长子序列】，而是【以num[i]结尾的子串长度最长为i】或者说【长度为i的递增子串中，末尾元素最小的是num[i]】。理解了这个问题以后就知道为什么新进来的元素要不就在末尾增加，要不就替代第一个大于等于它元素的位置。
这里的【替换】就蕴含了一个贪心的思想，对于同样长度的子串，我当然希望它的末端越小越好，这样以后我也有更多机会拓展。
[Open: Pasted image 20250316182621.png](%E7%AE%97%E6%B3%95/dp/_resources/%E7%BA%BF%E6%80%A7dp/5ab53b37b3d652583f54a71d2dd19706_MD5.jpeg)
![](%E7%AE%97%E6%B3%95/dp/_resources/%E7%BA%BF%E6%80%A7dp/5ab53b37b3d652583f54a71d2dd19706_MD5.jpeg)
```
/*
例 n: 7
arr : 3 1 2 1 8 5 6

stk : 3

1 比 3 小
stk : 1

2 比 1 大
stk : 1 2

1 比 2 小
stk : 1 2

8 比 2 大
stk : 1 2 8

5 比 8 小
stk : 1 2 5

6 比 5 大
stk : 1 2 5 6

stk 的长度就是最长递增子序列的长度


*/
```
核心在于不断维护更新序列的末端
```
#include<bits/stdc++.h>
using namespace std;
const int N = 1e5 + 5;

int a[N];
vector<int>num;
int main()
{
	ios::sync_with_stdio(0);
	cin.tie(0);
	cout.tie(0) ;
	int n;
	cin >> n;
	for (int i = 0; i < n; ++i) {
		
		cin >> a[i];
		if (num.empty() || a[i] > num.back())  num.push_back(a[i]);
		
		else {
			auto it = lower_bound(num.begin(), num.end(), a[i]);
			*it = a[i];
		}
	}
	
	cout << num.size();
	
	return 0;
 } 
```

# 最长公共子序列

[Open: Pasted image 20250320165620.png](%E7%AE%97%E6%B3%95/dp/_resources/%E7%BA%BF%E6%80%A7dp/e58a92ae0f357888f5ee826c61348caf_MD5.jpeg)
![](%E7%AE%97%E6%B3%95/dp/_resources/%E7%BA%BF%E6%80%A7dp/e58a92ae0f357888f5ee826c61348caf_MD5.jpeg)

[Open: Pasted image 20250320165640.png](%E7%AE%97%E6%B3%95/dp/_resources/%E7%BA%BF%E6%80%A7dp/0acb450d651003fe3b4d19fa6fe541fc_MD5.jpeg)
![](%E7%AE%97%E6%B3%95/dp/_resources/%E7%BA%BF%E6%80%A7dp/0acb450d651003fe3b4d19fa6fe541fc_MD5.jpeg)

```
#include <iostream>
using namespace std;
const int N = 1010;
int n, m;
char a[N], b[N];
int f[N][N];
int main() {
  cin >> n >> m >> a + 1 >> b + 1;
  for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= m; j++) {
      if (a[i] == b[j]) {
        f[i][j] = f[i - 1][j - 1] + 1;
      } else {
        f[i][j] = max(f[i - 1][j], f[i][j - 1]);
      }
    }
  }
  cout << f[n][m] << '\n';
  return 0;
}

作者：yuechen
链接：https://www.acwing.com/solution/content/8111/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```