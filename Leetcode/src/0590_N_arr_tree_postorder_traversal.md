# 590. N-ary Tree Postorder Traversal

## Description

Given an n-ary tree, return the postorder traversal of its nodes' values.

For example, given a 3-ary tree:

![](../images/590.png)

Return its postorder traversal as: [5,6,3,2,4,1].

 
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
    vector<int> postorder(Node* root) {
        if(root == nullptr)
            return {};
        vector<int> result;
        stack<Node *> s;
        s.push(root);
        while(!s.empty()){
            Node* temp = s.top();
            s.pop();
            for(auto it:temp->children){
                s.push(it);
            }
            result.push_back(temp->val);  
        }
        reverse(result.begin(), result.end());
        return result;
    }
};
```