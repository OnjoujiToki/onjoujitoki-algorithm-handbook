---
description: 如果有单调性肯定可以二分，但是可以二分的题目不一定非要有单调性。所以二分的本质不是单调性。
---

# 二分查找 Binary Search

从一到题开始&#x20;

#### [789. 数的范围](https://www.acwing.com/problem/content/791/)

给定一个按照升序排列的长度为 nn 的整数数组，以及 qq 个查询。

对于每个查询，返回一个元素 kk 的起始位置和终止位置（位置从 00 开始计数）。

如果数组中不存在该元素，则返回 `-1 -1`。

**输入格式**

第一行包含整数 nn 和 qq，表示数组长度和询问个数。

第二行包含 nn 个整数（均在 1∼100001∼10000 范围内），表示完整数组。

接下来 qq 行，每行包含一个整数 kk，表示一个询问元素。

**输出格式**

共 qq 行，每行包含两个整数，表示所求元素的起始位置和终止位置。

如果数组中不存在该元素，则返回 `-1 -1`。

**数据范围**

1≤n≤100000 1≤q≤10000 1≤k≤10000

**输入样例：**

```
6 3
1 2 2 3 3 4
3
4
5
```

**输出样例：**

```
3 4
5 5
-1 -1
```

```clike
#include <iostream>
using namespace std;
const int N = 1e5+10;
int m[N];
int p,n;
int bs2(int m[], int r, int t) {
    int l = 0;
    while (l  < r) {
        int mid = l +r >>1;
        if (t <= m[mid] ) r = mid;
        else l = mid +1 ;
    }
    return l ; 
}
int bs(int m[], int r, int t) {
    int l = 0;
    while (l  < r) {
        int mid = l + r +1>>1;
        if (t>=m[mid]) l = mid;
        else r = mid -1;
    }
    return l;
}
int main() {
    cin>> n>>p;
    for (int i = 0; i < n; i++) scanf("%d", &m[i]);
    for (int i = 0; i < p; i++) {
        int t;
        scanf("%d", &t);
        int l  = bs2(m, n -1,t);
        int r = bs(m, n -1, t);
        if (m[l] == t && m[r] == t)
            printf("%d %d\n", l ,r);
        else printf("-1 -1\n");
    }
}
```

模板理解。 bs2的是每次能把最右端的值完美切过来，bs1的话可以完美把左边的值切过来。

可以把 r = mid理解为反复往左边取值，把l = mid理解为反复往右边取值，分别对得到左端和右端的值！\


浮点数二分模板

```clike
bool check(double x) {/* ... */} // 检查x是否满足某种性质

double bsearch_3(double l, double r)
{
    const double eps = 1e-6;   // eps 表示精度，取决于题目对精度的要求
    while (r - l > eps)
    {
        double mid = (l + r) / 2;
        if (check(mid)) r = mid;
        else l = mid;
    }
    return l;
}

bool check(double x) {/* ... */} // 检查x是否满足某种性质

double bsearch_3(double l, double r)
{
    for (int i = 0; i < 100; i++)
    {
        double mid = (l + r) / 2;
        if (check(mid)) r = mid;
        else l = mid;
    }
    return l;
}
```

#### [790. 数的三次方根](https://www.acwing.com/problem/content/description/792/)

给定一个浮点数 nn，求它的三次方根。

**输入格式**

共一行，包含一个浮点数 nn。

**输出格式**

共一行，包含一个浮点数，表示问题的解。

注意，结果保留 66 位小数。

**数据范围**

−10000≤n≤10000−10000≤n≤10000

**输入样例：**

```
1000.00
```

**输出样例：**

```
10.000000
```

```clike
#include<iostream>
using namespace std;
double n;
double res;
int main() {
    cin>>n;
    double t = n;
    n = abs(n);
    double l  = 0;
    double r = n;
    if (n < 1) {
        l = t;
        r = 1;
        while(r-l > 1e-8) {
            double mid = (l+r)/2;
            if (mid * mid * mid >=n ) r = mid;
            else l =mid;
        }
    } else {
        while(r-l > 1e-8) {
            double mid = (l+r)/2;
            if (mid * mid * mid >=n ) r = mid;
            else l =mid;
      }  
        
    }
    if ( t <0) l = -l;
    printf("%lf\n",l);
    return 0;
}
```

思路：先转换成正数方便计算。

其次，分为0\~1和>1两种情况考虑。

0到1的话要从t到1之间进行二分。
