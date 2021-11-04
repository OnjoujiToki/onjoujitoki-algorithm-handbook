# Leetcode Template

一维

```clike
    vector<int> Bit; // 树状数组 Binary Indexed Tree
    int lowbit(int x) {
        return x & -x;
    }
    
    int getSum(int x) {
        int ans = 0;
        for (int i = x; i >= 1; i -= lowbit(i)) ans+= Bit[i];      
        return ans;
    }
    
    void add(int k, int v) {
        for (int i = k; i < Bit.size(); i += lowbit(i)) Bit[i] += v;
    }
```

二维

```clike
    vector<vector<int>> Bit;
    vector<vector<int>> matrix;
    int n, m;
    int lowbit(int x) {
        return x & (-x);
    }
    void add(int x, int y, int v) {
        for(int i = x; i <= n; i += lowbit(i)) {
            for (int j = y; j <= m; j += lowbit(j)) {
                Bit[i][j] += v;
            }
        }
    }
    
    int getSum(int x, int y) {
        int ans = 0;
        for (int i = x; i >= 1; i -= lowbit(i)) {
            for (int j = y; j >= 1; j -= lowbit(j)) {
                ans += Bit[i][j];     
            }
        }
        return ans;
    }    
```

