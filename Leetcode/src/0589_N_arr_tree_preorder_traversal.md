# 589. N-ary Tree Preorder Traversal

## Description

Given an n-ary tree, return the preorder traversal of its nodes' values.

For example, given a 3-ary tree:

![](../images/589.png)

Return its preorder traversal as: `[1,3,5,6,2,4]`.

 

Note:

Recursive solution is trivial, could you do it iteratively?

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
    vector<int> preorder(Node* root) {
        if(!root)  // 如果 root 为 null，直接返回
            return {};
        
        vector<int> res;
        
        stack<Node*> s;
        s.push(root);
        while(!s.empty()) {
            Node* node = s.top();
            s.pop();
            res.push_back(node->val);
            int n = node->children.size();
            for(int i = n-1; i >= 0; --i) {  // 首先将后面的child结点压入栈
                s.push(node->children[i]);
            }
        }
        
        return res;
    }
};
```