# Leetcode 模板

```cpp
class Trie {
public:
    struct Node {
        bool isEnd;
        Node* child[26];
        Node() {
            for (int i = 0; i <26;i++) {
                isEnd = false;
                child[i] = NULL;
            }
        }
    }*root;
    Trie() {
        root = new Node();
    }
    
    void insert(string word) {
        auto p = root;
        for (char c:word) {
            int u = c-'a';
            if(p->child[u] == NULL) p->child[u] = new Node();
            p = p->child[u];
        }
        p->isEnd = true;
    }
    
    bool search(string word) {
        auto p = root;
        for (char c:word) {
            if ( p->child[c- 'a'] == NULL) return false;
            p = p ->child[c- 'a'];
        }
        return p->isEnd;
    }
    
    bool startsWith(string prefix) {
        auto p = root;
        for (char c:prefix) {
            if (p->child[c-'a'] == NULL) return false;
            p = p -> child[c-'a'];
        }
        return true;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```
