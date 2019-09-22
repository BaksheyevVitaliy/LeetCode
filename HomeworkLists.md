# LeetCode_Lists

+ [Reorder List](#reorder-list)
+ [Linked List Cycle II](#linked-list-cycle-ii)
+ [Linked List Cycle](#linked-list-cycle)
+ [Merge Two Sorted Lists](#merge-two-sorted-lists)
+ [Remove Nth Node From End of List](#remove-nth-node-from-end-of-list)
+ [Middle of the Linked List](#middle-of-the-linked-list)
+ [Delete Node in a Linked List](#delete-node-in-a-linked-list)
+ [Palindrome Linked List](#palindrome-linked-list)
+ [Reverse Linked List](#reverse-linked-list)
+ [Remove Linked List Elements](#remove-linked-list-elements)
+ [Intersection of Two Linked Lists](#intersection-of-two-linked-lists)
+ [Sort List](#sort-list)

## Reorder List

https://leetcode.com/problems/reorder-list/

```C++
class Solution {
public:
    void reorderList(ListNode* head) {
        ListNode* cherepaha = head;
        ListNode* zayac = head;
        ListNode* first = NULL;
        ListNode* p = NULL;
        ListNode* q1 = NULL;
        
        
        if(zayac != NULL){
        while((zayac->next != NULL)&&(zayac->next->next != NULL)){
            cherepaha = cherepaha->next;
            zayac = zayac->next->next;            
        }
        q1 = cherepaha;
        cherepaha = cherepaha->next;
        q1->next = NULL;
        if(cherepaha != NULL){
        q1 = cherepaha->next;
        first = cherepaha;
        while(q1 != NULL){
            p = q1->next;
            q1->next = cherepaha;
            first->next = p;
            cherepaha = q1;
            q1 = p;        
        }
        zayac = head;
        q1 = zayac->next;
        p = cherepaha->next;
        while(q1 != NULL){
            zayac->next = cherepaha;
            cherepaha->next = q1;
            zayac = q1;
            cherepaha = p;
            q1 = q1->next;
            if(p != NULL)
                p = p->next;
        }
            zayac->next = cherepaha;
        }
        }
    }
};
```

## Linked List Cycle II

https://leetcode.com/problems/linked-list-cycle-ii/

```C++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* cherepaha = head;
        ListNode* zayac = head;
        
        
        if((zayac == NULL)||(zayac->next == NULL))
            return NULL;
        zayac = zayac->next;
        while((zayac->next != NULL)&&(zayac->next->next != NULL)&&(cherepaha != zayac)){
            cherepaha = cherepaha->next;
            zayac = zayac->next->next;  
        }
              if((zayac->next == NULL)||(zayac->next->next == NULL))
                return NULL;
              zayac = head;
              cherepaha = cherepaha->next;
              while(zayac != cherepaha){
                  cherepaha = cherepaha->next;
                  zayac = zayac->next;
              }
              return zayac;
    }
};
```

## Linked List Cycle

https://leetcode.com/problems/linked-list-cycle/

```C++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode* cherepaha = head;
        ListNode* zayac = head;
        
        
        if((zayac == NULL)||(zayac->next == NULL))
            return 0;
        zayac = zayac->next;
        while((zayac->next != NULL)&&(zayac->next->next != NULL)&&(cherepaha != zayac)){
            cherepaha = cherepaha->next;
            zayac = zayac->next->next;  
        }
              if((zayac->next == NULL)||(zayac->next->next == NULL))
                return 0;
        return 1;
        
    }
};
```

## Merge Two Sorted Lists

https://leetcode.com/problems/merge-two-sorted-lists/

```C++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* q1 = l1;
        ListNode* p1 = l2;
        ListNode* q = NULL;
        ListNode* first;
        if(q1 == NULL)
            return p1;
        if(p1 == NULL)
            return q1;
        if(q1->val <= p1->val){
            first = q1;
            q = q1;
            q1 = q1->next;
        }
        else{
            first = p1;
            q = p1;
            p1 = p1->next;
        }
        while((q1 != NULL)&&(p1 != NULL)){
            if(q1->val < p1->val){
                q->next = q1;
                q = q1;
                q1 = q1->next;
            }
            else{
                q->next = p1;
                q = p1;
                p1 = p1->next;
            }
            
        }
        if(q1 == NULL)
            q->next = p1;
        else
            q->next = q1;
        return first;
        
    }
};
```

## Remove Nth Node From End of List

https://leetcode.com/problems/remove-nth-node-from-end-of-list/

```C++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* q = head;
        ListNode* q1 = head;
        ListNode* p = head;
        
        if(q == NULL){
            return NULL;
        }
        if (n == 0)
            return head;
        while((n > 0)&&(q1 != NULL)){
            q1 = q1->next;
            n--;
        }
        if(q1 == NULL){
            p = q-> next;
            delete(q);
            return p;
        }
        while(q1->next != NULL){
            q1 = q1->next;
            q = q->next;            
        }
        p = q->next->next;
        delete(q->next);
        q->next = p;
        return head;
        
    }
};
```

## Middle of the Linked List

https://leetcode.com/problems/middle-of-the-linked-list/

```C++
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* cherepaha = head;
        ListNode* zayac = head;
        
        while((zayac->next != NULL)&&(zayac->next->next != NULL)){
            cherepaha = cherepaha->next;
            zayac = zayac->next->next;            
        }
        if(zayac->next == NULL)
            return cherepaha;
        return cherepaha->next;
        
    }
};
```

## Delete Node in a Linked List

https://leetcode.com/problems/delete-node-in-a-linked-list/

```C++
class Solution {
public:
    void deleteNode(ListNode* node) {
        ListNode* q = NULL;
        node->val = node->next->val;
        q = node->next;
        node->next = node->next->next;
        delete(q);
        
        
    }
};
```

## Palindrome Linked List

https://leetcode.com/problems/palindrome-linked-list/

```C++
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        ListNode* cherepaha = head;
        ListNode* zayac = head;
        ListNode* first = NULL;
        ListNode* p = NULL;
        ListNode* q1 = NULL;
        
        
        if(zayac == NULL)
            return 1;
        while((zayac->next != NULL)&&(zayac->next->next != NULL)){
            cherepaha = cherepaha->next;
            zayac = zayac->next->next;            
        }
        q1 = cherepaha;
        cherepaha = cherepaha->next;
        q1->next = NULL;
        if(cherepaha == NULL)
            return 1;
        q1 = cherepaha->next;
        first = cherepaha;
        while(q1 != NULL){
            p = q1->next;
            q1->next = cherepaha;
            first->next = p;
            cherepaha = q1;
            q1 = p;        
        }
        zayac = head;
        while(cherepaha != NULL){
            if(cherepaha->val != zayac->val)
                return 0;
            cherepaha = cherepaha->next;
            zayac= zayac->next;
        }
            return 1;
    }
};
```

## Reverse Linked List

https://leetcode.com/problems/reverse-linked-list/

```C++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* q = head;
        ListNode* first = head;
        ListNode* p = NULL;
        ListNode* q1 = NULL;
        
        if(q == NULL)
            return NULL;
        if(q->next == NULL)
            return head;
        q1 = q->next;
        while(q1 != NULL){
            p = q1->next;
            q1->next = q;
            first->next = p;
            q = q1;
            q1 = p;        
        }
        return q;
    }
};
```

## Remove Linked List Elements

https://leetcode.com/problems/remove-linked-list-elements/

```C++
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* q = head;
        ListNode* newhead = NULL;
        ListNode* q1 = NULL;
        ListNode* p = NULL;
        if(q == NULL)
            return NULL;
        while(q->val == val){
            if(q->next != NULL){
                q1 = q->next;
                delete(q);
                q = q1;
            }
            else
                return NULL;
        }
        q1 = q->next;
        newhead = q;
        while(q1 != NULL){
            if(q1->val == val){
                p = q1->next;
                delete(q1);
                q->next = p;
                q1 = p;
            }
            else{
                q = q1;
                q1 = q1->next;
            }
        }
        return newhead;
    }
};
```

## Intersection of Two Linked Lists

https://leetcode.com/problems/intersection-of-two-linked-lists/

```C++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* qA = headA;
        ListNode* qB = headB;
        ListNode* q = NULL;
        int sizeA = 0;
        int sizeB = 0;
        int size = 0;
        if((qA == NULL)||(qB == NULL))
            return NULL;
        while(qA != NULL){
            sizeA++;
            qA = qA->next;
        }
        while(qB != NULL){
            sizeB++;
            qB = qB->next;
        }
        size = sizeA - sizeB;
        qA = headA;
        qB = headB;
        if(size < 0){
            q = qB;
            size -=  2*size;
        }
        else
            q = qA;
        while(size > 0){
            q = q->next;
            size--;
        } 
        if(sizeA - sizeB < 0)
            qB = q;
        else
            qA = q;
        while((qA != qB)&&(qA != NULL)&&(qB != NULL)){
            qA = qA->next;
            qB = qB->next;
        }
        if((qA == NULL)||(qB == NULL))
            return NULL;
        return qA;
        
    }
};
```

## Sort List

https://leetcode.com/problems/sort-list/

```C++
class Solution {
public:
     ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* q1 = l1;
        ListNode* p1 = l2;
        ListNode* q = NULL;
        ListNode* first;
        if(q1 == NULL)
            return p1;
        if(p1 == NULL)
            return q1; 
        if(q1->val <= p1->val){
            first = q1;
            q = q1;
            q1 = q1->next;
        }
        else{
            first = p1;
            q = p1;
            p1 = p1->next;
        }
        while((q1 != NULL)&&(p1 != NULL)){
            if(q1->val < p1->val){
                q->next = q1;
                q = q1;
                q1 = q1->next;
            }
            else{
                q->next = p1;
                q = p1;
                p1 = p1->next;
            }
            
        }
        if(q1 == NULL)
            q->next = p1;
        else
            q->next = q1;
        return first;
        
    }


    ListNode* sortList(ListNode* head) {
        ListNode* q = NULL;
        ListNode* p = NULL;
        ListNode* p1 = NULL;
        ListNode* list_false = new ListNode(0);
        ListNode* list_head = head;
        ListNode* list_start = head;
        ListNode* list_end = head;
        ListNode* list1 = head;
        ListNode* end = head;
        int n = 1, length = 0, i = 0, j = 0, kostil = 0;
        while(list_head != NULL){
            list_head = list_head->next;
            length++;
        }
        list_head = head;
        list_false->next = list_head;
        while(n < length){
            q = list_head;
            list_start = list_false;
            list_end = q;
            p = list_false;     
            for(j = 0; j < length; j += 2 * n){
                for(i = 0; i < n * 2; i++){
                    if(list_end != NULL){
                        list_end = list_end->next;
                        p = p->next;
                    }
                    else
                        i = 2 * n;
                }
                p->next = NULL;
                p = q;
                kostil = 1;
                for(i = 0; i < n - 1; i++){
                    if(p->next != NULL)
                        p = p->next;
                    else
                        kostil = 0;
                }
                if (kostil){
                p1 = p;
                p = p->next;
                p1->next = NULL;
                list_start->next = NULL;
                list_start->next = mergeTwoLists(q, p);
                }
                while(list_start->next != NULL)
                    list_start = list_start->next;
                list_start->next = list_end;
                q = list_end;
                p = list_start;
                
                    
            }
            n *= 2;
            list_head = list_false->next;
        }
        delete(list_false);
        return list_head;    
        
    }
};
```
