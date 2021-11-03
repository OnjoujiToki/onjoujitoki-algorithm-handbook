# 剑指 Offer 26. 树的子结构

输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如: 给定的树 A:

&#x20;    3 &#x20;

&#x20; /      \\\
4        5   \
/  \\

1       2&#x20;

给定的树 B：

&#x20;  4  &#x20;

&#x20; /&#x20;

&#x20;1&#x20;

返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

示例 1：

输入：A = \[1,2,3], B = \[3,1] 输出：false 示例 2：

输入：A = \[3,4,5,1,2], B = \[4,1] 输出：true 限制：

`0 <= 节点个数 <= 10000`

```clike
class Solution {
public:
    bool dfs(TreeNode* A, TreeNode* B) {
        if (!B) return true;
        if (!A) return false;      
        if (A->val != B->val ) {
            return false;
        } 
        return dfs(A->left, B->left) && dfs(A->right, B->right);
    }
    bool isSubStructure(TreeNode* A, TreeNode* B) {
        if (!B || !A) return false;
        if (A->val == B->val && dfs(A,B)) return true;
        return isSubStructure(A->left, B) ||isSubStructure(A->right, B);
    }
};
```
