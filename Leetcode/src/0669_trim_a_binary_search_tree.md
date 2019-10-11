# 669. Trim a Binary Search Tree

## Description

Given a binary search tree and the lowest and highest boundaries as L and R, trim the tree so that all its elements lies in `[L, R]` (R >= L). You might need to change the root of the tree, so the result should return the new root of the trimmed binary search tree.

**Example 1:**

```
Input: 
    1
   / \
  0   2

  L = 1
  R = 2

Output: 
    1
      \
       2
```

**Example 2:**

```
Input: 
    3
   / \
  0   4
   \
    2
   /
  1

  L = 1
  R = 3

Output: 
      3
     / 
   2   
  /
 1
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
    TreeNode* trimBST(TreeNode* root, int L, int R) {
        while(root->val < L || root->val > R){
            if(root->val < L)
                root = root->right;
            else
                root = root->left;
        }
        
        TreeNode* left_ptr = root;
        TreeNode* right_ptr = root;
        
        while(left_ptr->left){
            if((left_ptr->left->val) < L){
                left_ptr->left = left_ptr->left->right;
            }else{
                left_ptr = left_ptr->left;
            }
        }
        while(right_ptr->right){
            if(right_ptr->right->val > R){
                right_ptr->right = right_ptr->right->left;
            }else{
                right_ptr = right_ptr->right;
            }
        }
        return root;
    }
};
```

```cpp
class Solution {
public:
    TreeNode* trimBST(TreeNode* root, int L, int R) {
        if (root == NULL) return NULL;
        if (root->val < L) return trimBST(root->right, L, R);
        if (root->val > R) return trimBST(root->left, L, R);
        root->left = trimBST(root->left, L, R);
        root->right = trimBST(root->right, L, R);
        return root;
    }
};
```