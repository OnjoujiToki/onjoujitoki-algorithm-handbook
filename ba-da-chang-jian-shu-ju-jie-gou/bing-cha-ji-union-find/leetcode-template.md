# Leetcode Template

自用的面试版本并查集

```clike
private:
    vector<int> sz;
    vector<int> id;
    int root(int i) {
        while(i != id[i]) {
            id[i] = id[id[i]];
            i = id[i];
        }
        return i;
    }
    bool isConnected(int i, int j) {
        return root(i) == root(j);
    }
    bool merge(int p, int q) {
        int i = root(p);
        int j = root(q);
        if (i == j) return false;
        if (sz[i] < sz[j]) {
            sz[j] += sz[i];
            id[i] = j;
        } else {
            sz[i] +=sz[j];
            id[j] = i;
        }
        return true;
    }
```





零神的并查集模板

[https://leetcode-cn.com/problems/graph-connectivity-with-threshold/solution/dai-yu-zhi-de-tu-lian-tong-xing-by-zerotrac2/](https://leetcode-cn.com/problems/graph-connectivity-with-threshold/solution/dai-yu-zhi-de-tu-lian-tong-xing-by-zerotrac2/)

```clike
class UF {
public:
    vector<int> fa;
    vector<int> sz;
    int n;
    int comp_cnt;
    
public:
    UF(int _n): n(_n), comp_cnt(_n), fa(_n), sz(_n, 1) {
        iota(fa.begin(), fa.end(), 0);
    }
    
    int findset(int x) {
        return fa[x] == x ? x : fa[x] = findset(fa[x]);
    }
    
    void unite(int x, int y) {
        x = findset(x);
        y = findset(y);
        if (x != y) {
            if (sz[x] < sz[y]) {
                swap(x, y);
            }
            fa[y] = x;
            sz[x] += sz[y];
            --comp_cnt;
        }
    }
    
    bool connected(int x, int y) {
        x = findset(x);
        y = findset(y);
        return x == y;
    }
};

作者：zerotrac2
链接：https://leetcode-cn.com/problems/graph-connectivity-with-threshold/solution/dai-yu-zhi-de-tu-lian-tong-xing-by-zerotrac2/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```
