# 206. Reverse Linked List

## Description

Reverse a singly linked list.

**Example:**

```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

**Follow up:**

- A linked list can be reversed either iteratively or recursively. Could you implement both?

## Solution

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *p = NULL;
        ListNode* cur = head;
        ListNode* post;
        while(cur) {
            post = cur->next;
            cur->next = p;
            p = cur;
            cur = post;
        }
        
        return p;
        
    }
};
```

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(!head || !(head->next))
            return head;
        
        ListNode* node = reverseList(head->next);
        head->next->next = head;
        head->next = NULL;
        return node;
        
    }
};
```