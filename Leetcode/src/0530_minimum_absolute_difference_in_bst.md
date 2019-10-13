# 530. Minimum Absolute Difference in BST

## Description

Given a binary search tree with non-negative values, find the minimum absolute difference between values of any two nodes.

**Example:**

```
Input:

   1
    \
     3
    /
   2

Output:
1

Explanation:
The minimum absolute difference is 1, which is the difference between 2 and 1 (or between 2 and 3).
```

**Note:** There are at least two nodes in this BST.

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
    int getMinimumDifference(TreeNode* root) {
        int min_diff = INT_MAX;
        TreeNode* pre = nullptr;
        inorder(root, pre, min_diff);
        return min_diff;
    }
    
    void inorder(TreeNode* root, TreeNode*& pre, int& min_diff) {
        if(root->left)
            inorder(root->left, pre, min_diff);
        
        if(pre)
            min_diff = min(min_diff, abs(root->val - pre->val));
        
        pre = root;
        
        if(root->right)
            inorder(root->right, pre, min_diff);
    }
};
```