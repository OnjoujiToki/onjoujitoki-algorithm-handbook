---
description: 琪露诺是在妖精中能力十分突出的。
---

# 快速排序 Quick Sort

[**912. 排序数组**](https://leetcode-cn.com/problems/sort-an-array/)

快速排序->先整体有序后局部有序

为什么等于pivot的既可以在左边又可以在右边？

为了防止在排序中出现极端情况，比如数组中很多数一样，不能严格小于or大于(left <= right 而不是 left < right)，否则在partition后不是很均匀。

1. 确定分界点 q\[l], q\[(l+r)/2], q\[r] 随机
2. 调整区间 使得第一个区间的所有数都小于等于x,第二个区间的所有数都大大于等于x
3. 递归
4. 递归处理左右两边

一个重点是l和r在最后结束的时候要进行移位，所以在递归后大概是这个模样

```
quick_sort(q, l, j);
quick_sort(q, j + 1, r);
```

方法一: O(n) 比较暴力

1. a\[], b\[]
2. 比较pivot，插入a 或者 b
3. 需要一些额外空间

方法二：优美做法

用2个指针，同时往中间走，如果符合要求，就先移动，如果不符合，就移动r然后交换

相遇之后，就分好了

```cpp
#include <iostream>

using namespace std;

const int N = 1e6 + 10;
int n;
int q[N];

void quick_sort(int q[], int l, int r)
{
    //递归的终止情况
    if(l >= r) return;
    //第一步：分成子问题
    int i = l - 1, j = r + 1, x = q[l + r >> 1];
    while(i < j)
    {
        do i++; while(q[i] < x);
        do j--; while(q[j] > x);
        if(i < j) swap(q[i], q[j]);
    }
    //第二步：递归处理子问题
    quick_sort(q, l, j), quick_sort(q, j + 1, r);
    //第三步：子问题合并.快排这一步不需要操作，但归并排序的核心在这一步骤
}
// https://www.acwing.com/solution/content/16777/ 非常不错的边界分析
int main() {
    scanf("%d", &n);
    int l = 0, r = n - 1 ;
    for (int i = 0; i < n; i++) scanf("%d", &q[i]);
    quick_sort(q, l, r);
    for (int i = 0; i < n; i++) printf("%d ", q[i]);
    return 0;
}


```

```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        if (nums.size() == 0) return nums;
        quickSort(nums, 0 , nums.size()-1);
        return nums;
    }
    void quickSort(vector<int>& nums, int start, int end) {
        if (start >= end) return;
        int left = start -1 ;
        int right = end + 1;
        int pivot = nums [ start + end >> 1];
        while(left < right) {
            do left++ ; while (nums[left] < pivot);
            do right--; while (nums[right] > pivot);
            if (left < right) swap(nums[left], nums[right]);
        }
        quickSort(nums, start, right);
        quickSort(nums, right + 1, end);
    }
};
```

\
