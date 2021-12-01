# More

##

```c
class Solution {
public:
    bool equationsPossible(vector<string>& equations) {
        for (int i = 0; i <26; i++) {
            id.push_back(i);
            sz.push_back(1);
        }
        for(auto x:equations) {
            if(x[1] == '=') {
                // == situation;
                unionF(x[0]-97, x[3]-97);
                //cout<<x[0]-97 <<" " << x[3]-97<< endl;
            }
        }
        for (auto x:equations) {
            if (x[1] == '!') {
                // != situation
                if (isConnected(x[0]-97,x[3]-97)) return false;
            }
        } 
        return true;

    }

private:
    vector<int>id;
    vector<int>sz;
    int root(int i) {
        while (id[i] != i) {
            // path compression
            id[i] = id[id[i]];
            i = id[i];
        }
        return i;
    }

    bool isConnected(int p, int q) {
        return root(p) == root(q);
    }
    
    void unionF (int p, int q) {
        int i = root(p);
        int j = root(q);
        if (i == j) return; 
        if (sz[i] < sz[j]) {
            sz[j]+= sz[i];
            id[i] = j;
        } else {
            sz[i] += sz[j];
            id[j] = i;
        }
        return;
    }
    
};
```

这道题其实没啥难点。需要记住的东西是如何把字母a转换成数字0， z转换成25这个样子。

很简单，减去97就好。如果想把0-26转换成26个小写字母，则可以

```
cout<< char(0+97)<<endl;
```

## [684. Redundant Connection](https://leetcode-cn.com/problems/redundant-connection/)

```clike
class Solution {
public:
    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        vector<int> res;
        for (int i = 0; i <edges.size(); i++) {
            id.push_back(i);
            sz.push_back(1);
        }
        for(auto vi: edges) {
            if (!isConnected(vi[0]-1,vi[1]-1)) unionF(vi[0]-1, vi[1]-1);
            else {
                res.clear();
                res.push_back(vi[0]);
                res.push_back(vi[1]);
            }
        }
        return res;
        
    }

private:
    vector<int>id;
    vector<int>sz;
    int root(int i) {
        while (id[i] != i) {
            // path compression
            id[i] = id[id[i]];
            i = id[i];
        }
        return i;
    }

    bool isConnected(int p, int q) {
        return root(p) == root(q);
    }
    
    void unionF (int p, int q) {
        int i = root(p);
        int j = root(q);
        
        if (i == j) return; 
        if (sz[i] < sz[j]) {
            sz[j]+= sz[i];
            id[i] = j;
        } else {
            sz[i] += sz[j];
            id[j] = i;
        }
        return;
    }
    
};
```

注意的点是这个节点的数字是从1开始的就很坑。所以为了使用并查集的坐标和value初始化时一一对应的这个特征，如果不想修改并查集，最好的方法那还是直接-1。如果是其他的题，比如上一题，想办法转换为0为开头的即可。附上另外一种方法，在初始化的时候就直接修改并查集的对应值。

## [1319. Number of Operations to Make Network Connected](https://leetcode-cn.com/problems/number-of-operations-to-make-network-connected/)

```c
class Solution {
public:
    int makeConnected(int n, vector<vector<int>>& connections) {
        cable = 0; // extra cable
        countofConnected = 1;
        for(int i = 0; i <n; i++) {
            id.push_back(i);
            sz.push_back(1);
        }
        for (auto vi:connections) {
            unionF(vi[0],vi[1]);
        }
        //成功做了三次union，其实连了4个。。所以初始化的时候要是1
        cout<<countofConnected<<cable;
        if (n-countofConnected> cable ) {
            return -1;
        }
        else return n-countofConnected;
        

    }
private:
    int cable;
    int countofConnected;
    // find 1 computer sz equals one.
    vector<int>id;
    vector<int>sz;
    int root(int i) {
        while (id[i] != i) {
            // path compression
            id[i] = id[id[i]];
            i = id[i];
        }
        return i;
    }

    bool isConnected(int p, int q) {
        return root(p) == root(q);
    }
    
    void unionF (int p, int q) {
        int i = root(p);
        int j = root(q);
        if (i == j) {
            // we got a extra cable;
            cable++;
            return;
        }
        if (sz[i] < sz[j]) {
            sz[j]+= sz[i];
            id[i] = j;
        } else {
            sz[i] += sz[j];
            id[j] = i;
        }
        countofConnected++;
        return;
    }
    
};
```

不能用sz来做这个事情，因为很多sz依然是1...感觉这个C++的实现可以再改得范用一点

还有就是，union三次，会连4个电脑。。不是三个，脑残了。

## [765. Couples Holding Hands](https://leetcode-cn.com/problems/couples-holding-hands/)

```c
class Solution {
public:
    int minSwapsCouples(vector<int>& row) {
        // 这题能想到并查集也是蛮不容易的。。。
        // we treat two people who are seating tgt as one node
        // if two nodes connect into one tree
        // which means, they all in the wrong position
        // so we can just swap once.
        // gogo union find!
        count = 0;
        int length = row.size();
        if (length <= 2) return 0;
        for (int i = 0; i < length/2; i++) {
            id.push_back(i);
            sz.push_back(1);
        }
        for (int i = 0; i < length; i = i +2) {
            unionF(row[i]>>1,row[i+1]>>1);
        }
       
        return count;
    }
private:
    vector<int> id;
    vector<int> sz;
    int count;
    int root(int i) {
        while(i!= id[i]) {
            id[i] = id[id[i]]; // path compression
            i= id[i];
        }
        return i;
    }
    
    void unionF(int p, int q) {
        int i = root(p);
        int j = root(q);
        
        if (i == j) return;
        if (sz[i]<sz[j]) {
            sz[j] += sz[i];
            id[i] = j;
        } else {
            sz[i] += sz[j];
            id[j] = i;
        }

        count++;
        return;
    }
};
```

这题还是挺有意思的。要把1对情侣转换成一个节点。如果他们有一对错情侣，一定有另外一对。而且相邻的情侣，如果坐的是对的，除2的时候都是一个值。

这道题，如果有一对情侣坐错了，大概就是union(i, j) 但是i 不等于j。

如果没坐错，那个这个union是失败的。

All we need to do，就是找到有几个环，然后减去1就是需要的答案。

不错的题解：[为什么交换任意一个都是对的？两种 100% 的解法：并查集 & 贪心](https://leetcode-cn.com/problems/couples-holding-hands/solution/liang-chong-100-de-jie-fa-bing-cha-ji-ta-26a6/)
