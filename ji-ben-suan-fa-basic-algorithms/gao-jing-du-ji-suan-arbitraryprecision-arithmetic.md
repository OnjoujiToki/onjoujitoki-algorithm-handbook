# 高精度计算 Arbitrary-Precision Arithmetic

#### 高精度常见mode

A + B 10^6

A - B 10^6

A \* a len(A) <=10^6 a<=1000

A/a

大整数存储 ->每一位存到数组 低位在前，高位在后ode

[AcWing 791. 高精度加法](https://www.acwing.com/problem/content/793/)

```clike
c#include <iostream>
#include <vector>
#include <string>
using namespace std;
const int N = 1e5+10;
string a,b;

vector<int> add(vector<int> &A, vector<int> &B) {
    vector<int> C;
    int t = 0; 
    for (int i = 0; i < A.size() || i < B.size(); i++) {
        if (i < A.size()) t+= A[i];
        if (i < B.size()) t+= B[i];
        C.push_back(t%10);
        t /= 10; //进位
    }
    if (t) C.push_back(1); // 如果还有进位
    return C;
}
int main() {
    cin >> a >>b;
    vector<int>A,B;
    for (int i = a.size() -1; i>= 0;i -- ) {
        A.push_back(a[i]-'0');
    }
    for (int i = b.size() -1;i>= 0;i -- ) {
        B.push_back(b[i]-'0');
    }
    auto C = add(A,B);
    for (int i = C.size() -1; i>=0;i--) {
        printf("%d", C[i]);
    }
    return 0;
}
```

高精度减法稍微复杂一点，但是可以用大的数减去小的数再考虑要不要补减号的方式消除很多很多的边界情况。

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;
const int N = 1e5+10;
string a,b;

bool cmp (vector<int>& A, vector<int>&B) {
    if (A.size() > B.size()) return true; 
    if (A.size() < B.size()) return false;
    for (int i = A.size() -1; i>=0; i--) {
        if (A[i]!=B[i]) return A[i] >B[i];
    }
    
    return true;
    
}
vector<int> substract(vector<int> &A, vector<int> &B) {
    vector<int> C;
    int t = 0; 
    for (int i = 0; i < A.size();i++) { // A.size() > B.size()
        t = A[i]-t;
        if (i < B.size()) t -= B[i];
        
        if (t >=0) C.push_back(t);
        else C.push_back(t+10); // can be (t+10)%10
        
        if (t<0) t= 1;
        else t =0;
    }
    while (C.size() > 1 && C.back() == 0) {
        C.pop_back(); // removing leading zeroes
    }
    
   
    return C;
}
int main() {
    cin >> a >>b;
    vector<int>A,B;
    for (int i = a.size() -1; i>= 0;i -- ) {
        A.push_back(a[i]-'0');
    }
    for (int i = b.size() -1;i>= 0;i -- ) {
        B.push_back(b[i]-'0');
    }
    if(cmp(A,B)) {
        auto C = substract(A,B);
        for (int i = C.size() -1; i>=0;i--) 
            printf("%d", C[i]);
    } else {
        auto C = substract(B,A);
        printf("-");
        for (int i = C.size() -1; i>=0;i--) 
            printf("%d", C[i]);
    }
    
    return 0;
}
```
