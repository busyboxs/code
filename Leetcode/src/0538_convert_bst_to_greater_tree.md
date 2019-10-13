# 538. Convert BST to Greater Tree

## Description

Given a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus sum of all keys greater than the original key in BST.

**Example:**

```
Input: The root of a Binary Search Tree like this:
              5
            /   \
           2     13

Output: The root of a Greater Tree like this:
             18
            /   \
          20     13
```

## Solution

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* convertBST(TreeNode* root) {
        if(!root)
            return root;
        stack<TreeNode*> s;
        TreeNode* p = root;
        int temp = 0;  // accumulate sum of processed node.
        while(!s.empty() || p){
            while(p){  // find node with largest value of the tree node not processed
                s.push(p);
                p = p->right;
            }
            if(!s.empty()){
                p = s.top();
                s.pop();
                p->val += temp;
                temp = p->val;
                p = p->left;  
            }
        }
        return root;
    }
};
```