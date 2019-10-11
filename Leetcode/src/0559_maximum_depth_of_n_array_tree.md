# 559. Maximum Depth of N-ary Tree

## Description

Given a n-ary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

For example, given a `3-ary` tree:

 ![](../images/559.png)

We should return its max depth, which is 3.

**Note:**

- The depth of the tree is at most 1000.
- The total number of nodes is at most 5000.

## Solution

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
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
    int maxDepth(Node* root) {
        if(root == nullptr)
            return 0;
        queue<Node*> q;
        q.push(root);
        int depth = 0;
        while(!q.empty()){
            depth += 1;
            int breadth = q.size();
            for(int i = 0; i < breadth; ++i){
                Node* node = q.front();
                q.pop();
                for(auto it: node->children){
                    q.push(it);
                }
            }
        }
        return depth;
    }
};
```