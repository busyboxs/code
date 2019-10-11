# 226. Invert Binary Tree

## Description

Invert a binary tree.

**Example:**

```
Input:

     4
   /   \
  2     7
 / \   / \
1   3 6   9
Output:

     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

**Trivia:**

This problem was inspired by this original tweet by Max Howell:

> Google: 90% of our engineers use the software you wrote (Homebrew), but you can’t invert a binary tree on a whiteboard so f*** off.

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
    TreeNode* invertTree(TreeNode* root) {
        if(!root)
            return root;
        TreeNode* p = root;
        TreeNode* result = p;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()){
            int breadth = q.size();
            for(int i = 0; i < breadth; ++i){
                TreeNode* node = q.front();
                q.pop();
                TreeNode* Nl = node->left;
                node->left = node->right;
                node->right = Nl;
                if(node->left){
                    q.push(node->left);
                }  
                if(node->right){
                    q.push(node->right);
                }  
                     
            }
        }
        return result;
    }
};
```