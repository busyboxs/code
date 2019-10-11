# 429. N-ary Tree Level Order Traversal

## Description

Given an n-ary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example, given a `3-ary` tree:
 
![](../images/429.png)

We should return its level order traversal:

```
[
     [1],
     [3,2,4],
     [5,6]
]
```

**Note:**

- The depth of the tree is at most 1000.
- The total number of nodes is at most 5000.

## Solution

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val = NULL;
    vector<Node*> children;

    Node() {}

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Solution {
public:
    vector<vector<int>> levelOrder(Node* root) {
        if(!root)
            return {};
        vector<vector<int>> v;
        queue<Node*> q;
        q.push(root);
        while(!q.empty()){
            int breadth = q.size();
            vector<int> temp;
            for(int i = 0; i < breadth; ++i){
                Node* node = q.front();
                q.pop();
                temp.push_back(node->val);
                for(auto child:node->children){
                    q.push(child);
                }
            }
            v.push_back(temp);
            
        }
        return v;
    }
};
```