# 653. Two Sum IV - Input is a BST

## Description

Given a Binary Search Tree and a target number, return true if there exist two elements in the BST such that their sum is equal to the given target.

**Example 1:**

```
Input: 
    5
   / \
  3   6
 / \   \
2   4   7

Target = 9

Output: True
```

**Example 2:**

```
Input: 
    5
   / \
  3   6
 / \   \
2   4   7

Target = 28

Output: False
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
    bool dfs(TreeNode* root, unordered_set<int>& s, int k){
        if(!root)
            return false;
        if(s.count(k - root->val))
            return true;
        s.insert(root->val);
        return dfs(root->left, s, k) || dfs(root->right, s, k);
    }
    
    bool findTarget(TreeNode* root, int k) {
        unordered_set<int> s;
        return dfs(root, s, k);
    }
};
```