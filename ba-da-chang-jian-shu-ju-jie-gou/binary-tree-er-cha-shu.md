---
description: 献给已逝公主的七重奏
cover: >-
  https://images.unsplash.com/photo-1519389950473-47ba0277781c?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=2970&q=80
coverY: 0
---

# Binary Tree 二叉树

{% hint style="info" %}
**Good to know:** It is always great to learn Binary Tree before going deep into recursion and Depth-first search.
{% endhint %}

### Breadth-First Search

有3种方法可以做到二叉树的BFS，分别是用dummy node思想，size思想，以及双queue思想。

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



{% hint style="info" %}
**Good to know:** Encourage employees to write a succinct bio that can help new hires learn about them and how they like to work.
{% endhint %}
