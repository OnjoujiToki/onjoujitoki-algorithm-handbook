---
description: 献给已逝公主的七重奏
cover: >-
  https://images.unsplash.com/photo-1519389950473-47ba0277781c?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=2970&q=80
coverY: 0
---

# 二叉树 Binary Tree

{% hint style="info" %}
**Good to know:** It is always great to learn Binary Tree before going deep into recursion and Depth-first search.
{% endhint %}

### Breadth-First Search

有3种方法可以做到二叉树的BFS，分别是用dummy node思想，size思想，以及双queue思想。其中最常用也最好用的莫过于第二种，省时省力。

```python
 class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:
            return []
        queue = deque([root,None]) # initialize root and None
        results, level = [], []
        while queue:
            node = queue.popleft()
            if node is None: # we met dummy node
                results.append(level)
                level = []
                if queue:
                    queue.append(None)
                continue
            level.append(node.val)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        return results
```

```go
func levelOrder(root *TreeNode) [][]int {
    if root == nil {
        return [][]int{} 
    }
    queue := []*TreeNode{root}
    res := make([][]int, 0)
    for (len(queue) > 0) {
        size := len(queue)
        level := make([]int,0)
        for i:= 0; i < size; i++ {
            if queue[i].Left != nil {
                queue = append(queue, queue[i].Left)
            }
            if queue[i].Right != nil {
                queue = append(queue, queue[i].Right)
            }
            level = append(level, queue[i].Val)
        }
        queue = queue[size:] // remove all poped elements
        res = append(res, level)
    }
    return res
}
```

```python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:
            return []
        queue = [root] # initialize root and None
        results = []
        while queue:
            another_queue = []
            results.append([node.val for node in queue]) # new a list then append in queue
            for node in queue:
                if node.left:
                    another_queue.append(node.left)
                if node.right:
                    another_queue.append(node.right)
            queue = another_queue
        return results
```
