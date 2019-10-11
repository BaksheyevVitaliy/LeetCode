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
        ListNode* slow = head;
        ListNode* fast = head;
        ListNode* first = NULL;
        ListNode* passing = NULL;
        ListNode* buff = NULL;
        
        
        if(fast != NULL){                                      //find middle
        while((fast->next != NULL)&&(fast->next->next != NULL)){
            slow = slow->next;
            fast = fast->next->next;            
        }
        buff = slow;                                          //reverse 2-nd half
        slow = slow->next;
        buff->next = NULL;
        if(slow != NULL){
        buff = slow->next;
        first = slow;
        while(buff != NULL){
            passing = buff->next;
            buff->next = slow;
            first->next = passing;
            slow = buff;
            buff = passing;        
        }
        fast = head;
        buff = fast->next;
        passing = slow->next;
        while(buff != NULL){                                //reorder list
            fast->next = slow;
            slow->next = buff;
            fast = buff;
            slow = passing;
            buff = buff->next;
            if(passing != NULL)
                passing = passing->next;
        }
            fast->next = slow;
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
        ListNode* slow = head;
        ListNode* fast = head;
        
        
        if((fast == NULL)||(fast->next == NULL))
            return NULL;
        fast = fast->next;
        while((fast->next != NULL)&&(fast->next->next != NULL)&&(slow != fast)){                 //detect cicle
            slow = slow->next;
            fast = fast->next->next;  
        }
              if((fast->next == NULL)||(fast->next->next == NULL))                     
                return NULL;
              fast = head;
              slow = slow->next;
              while(fast != slow){                                                               //find cicle
                  slow = slow->next;
                  fast = fast->next;
              }
              return fast;
    }
};
```

## Linked List Cycle

https://leetcode.com/problems/linked-list-cycle/

```C++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode* slow = head;
        ListNode* fast = head;
        
        
        if((fast == NULL)||(fast->next == NULL))
            return false;
        fast = fast->next;
        while((fast->next != NULL)&&(fast->next->next != NULL)&&(slow != fast)){           //detect cicle
            slow = slow->next;
            fast = fast->next->next;  
        }
              if((fast->next == NULL)||(fast->next->next == NULL))
                return false;
        return true;
        
    }
};
```

## Merge Two Sorted Lists

https://leetcode.com/problems/merge-two-sorted-lists/

```C++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* PassingList1 = l1;
        ListNode* PassingList2 = l2;
        ListNode* AlreadySort = NULL;
        ListNode* head;
        if(PassingList1 == NULL)
            return PassingList2;
        if(PassingList2 == NULL)
            return PassingList1;
        if(PassingList1->val <= PassingList2->val){
            head = PassingList1;
            AlreadySort = PassingList1;
            PassingList1 = PassingList1->next;
        }
        else{
            head = PassingList2;
            AlreadySort = PassingList2;
            PassingList2 = PassingList2->next;
        }
        while((PassingList1 != NULL)&&(PassingList2 != NULL)){
            if(PassingList1->val < PassingList2->val){
                AlreadySort->next = PassingList1;
                AlreadySort = PassingList1;
                PassingList1 = PassingList1->next;
            }
            else{
                AlreadySort->next = PassingList2;
                AlreadySort = PassingList2;
                PassingList2 = PassingList2->next;
            }
            
        }
        if(PassingList1 == NULL)
            AlreadySort->next = PassingList2;
        else
            AlreadySort->next = PassingList1;
        return head;
        
    }
};
```

## Remove Nth Node From End of List

https://leetcode.com/problems/remove-nth-node-from-end-of-list/

```C++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* PassList = head;
        ListNode* PassListAfterN = head;
        ListNode* buff = head;
        
        if(PassList == NULL){
            return NULL;
        }
        if (n == 0)
            return head;
        while((n > 0)&&(PassListAfterN != NULL)){
            PassListAfterN = PassListAfterN->next;
            n--;
        }
        if(PassListAfterN == NULL){
            buff = PassList-> next;
            delete(PassList);
            return buff;
        }
        while(PassListAfterN->next != NULL){
            PassListAfterN = PassListAfterN->next;
            PassList = PassList->next;            
        }
        buff = PassList->next->next;
        delete(PassList->next);
        PassList->next = buff;
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
        ListNode* slow = head;
        ListNode* fast = head;
        
        while((fast->next != NULL)&&(fast->next->next != NULL)){
            slow = slow->next;
            fast = fast->next->next;            
        }
        if(fast->next == NULL)
            return slow;
        return slow->next;
        
    }
};
```

## Delete Node in a Linked List

https://leetcode.com/problems/delete-node-in-a-linked-list/

```C++
class Solution {
public:
    void deleteNode(ListNode* node) {
        ListNode* DeletedList = NULL;
        node->val = node->next->val;
        DeletedList = node->next;
        node->next = node->next->next;
        delete(DeletedList);
        
        
    }
};
```

## Palindrome Linked List

https://leetcode.com/problems/palindrome-linked-list/

```C++
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        ListNode* slow = head;
        ListNode* fast = head;
        ListNode* first = NULL;
        ListNode* buff = NULL;
        ListNode* PassHalf = NULL;
        
        
        if(fast == NULL)
            return true;
        while((fast->next != NULL)&&(fast->next->next != NULL)){
            slow = slow->next;
            fast = fast->next->next;            
        }
        PassHalf = slow;
        slow = slow->next;
        PassHalf->next = NULL;
        if(slow == NULL)
            return true;
        PassHalf = slow->next;
        first = slow;
        while(PassHalf != NULL){
            buff = PassHalf->next;
            PassHalf->next = slow;
            first->next = buff;
            slow = PassHalf;
            PassHalf = buff;        
        }
        fast = head;
        while(slow != NULL){
            if(slow->val != fast->val)
                return false;
            slow = slow->next;
            fast= fast->next;
        }
            return true;
    }
};
```

## Reverse Linked List

https://leetcode.com/problems/reverse-linked-list/

```C++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* HeadOfNewList = head;
        ListNode* TailOfNewList = head;
        ListNode* FirstOfOldList = NULL;
        
        if(HeadOfNewList == NULL)
            return NULL;
        if(HeadOfNewList->next == NULL)
            return head;
        FirstOfOldList = HeadOfNewList->next;
        while(FirstOfOldList != NULL){
            TailOfNewList->next = TailOfNewList->next->next;
            FirstOfOldList->next = HeadOfNewList;
            HeadOfNewList = FirstOfOldList;
            FirstOfOldList = TailOfNewList->next;        
        }
        return HeadOfNewList;
    }
};
```

## Remove Linked List Elements

https://leetcode.com/problems/remove-linked-list-elements/

```C++
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* PassFirst = head;
        ListNode* NewHead = head;
        ListNode* PassNext = NULL;
        ListNode* DeleteBuff = NULL;
        if(NewHead == NULL)
            return NULL;
        while(NewHead->val == val){
            if(NewHead->next != NULL){
                PassNext = NewHead->next;
                delete(NewHead);
                NewHead = PassNext;
            }
            else
                return NULL;
        }
        PassFirst = NewHead;
        PassNext = PassFirst->next;
        while(PassNext != NULL){
            if(PassNext->val == val){
                DeleteBuff = PassNext->next;
                delete(PassNext);
                PassFirst->next = DeleteBuff;
                PassNext = DeleteBuff;
            }
            else{
                PassFirst = PassNext;
                PassNext = PassNext->next;
            }
        }
        return NewHead;
    }
};
```

## Intersection of Two Linked Lists

https://leetcode.com/problems/intersection-of-two-linked-lists/

```C++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* PassA = headA;
        ListNode* PassB = headB;
        if((PassA == NULL)||(PassB == NULL))
            return NULL;
        while(PassA != PassB){
            if((PassA == NULL)||(PassB == NULL)){
                if(PassA == NULL)
                    PassA = headB;
                if(PassB == NULL)
                    PassB = headA;
            }
            else{
                PassA = PassA->next;
                PassB = PassB->next;
        }
        }
        return PassA;
        
    }
};
```

## Sort List

https://leetcode.com/problems/sort-list/

```C++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* PassingList1 = l1;
        ListNode* PassingList2 = l2;
        ListNode* AlreadySort = NULL;
        ListNode* head;
        if(PassingList1 == NULL)
            return PassingList2;
        if(PassingList2 == NULL)
            return PassingList1;
        if(PassingList1->val <= PassingList2->val){
            head = PassingList1;
            AlreadySort = PassingList1;
            PassingList1 = PassingList1->next;
        }
        else{
            head = PassingList2;
            AlreadySort = PassingList2;
            PassingList2 = PassingList2->next;
        }
        while((PassingList1 != NULL)&&(PassingList2 != NULL)){
            if(PassingList1->val < PassingList2->val){
                AlreadySort->next = PassingList1;
                AlreadySort = PassingList1;
                PassingList1 = PassingList1->next;
            }
            else{
                AlreadySort->next = PassingList2;
                AlreadySort = PassingList2;
                PassingList2 = PassingList2->next;
            }
            
        }
        if(PassingList1 == NULL)
            AlreadySort->next = PassingList2;
        else
            AlreadySort->next = PassingList1;
        return head;
        
    }


    ListNode* sortList(ListNode* head) {
        ListNode* HeadOfFirstMergeLists = NULL;
        ListNode* HeadOfSecondMergeLists = NULL;
        ListNode* buff = NULL;
        ListNode* ListFalse = new ListNode(0);                     //list before head
        ListNode* ListHead = head;
        ListNode* ListStart = head;                               //list before merge lists
        ListNode* ListEnd = head;                                 //list after merge lists
        int n = 1, length = 0, i = 0, j = 0;
        bool FlagHaveSecondHalf = true;
        while(ListHead != NULL){
            ListHead = ListHead->next;
            length++;
        }
        ListHead = head;
        ListFalse->next = ListHead;
        while(n < length){                                       
            HeadOfFirstMergeLists = ListHead;
            ListStart = ListFalse;
            ListEnd = ListHead;
            HeadOfSecondMergeLists = ListFalse;     
            for(j = 0; j < length; j += 2 * n){
                for(i = 0; i < n * 2; i++){                             // split into pieces of length 2 * n
                    if(ListEnd != NULL){
                        ListEnd = ListEnd->next;
                        HeadOfSecondMergeLists = HeadOfSecondMergeLists->next;
                    }
                    else
                        i = 2 * n;
                }
                HeadOfSecondMergeLists->next = NULL;
                HeadOfSecondMergeLists = HeadOfFirstMergeLists;
                FlagHaveSecondHalf = true;
                for(i = 0; i < n - 1; i++){                           //merge into 2 pieces of length n
                    if(HeadOfSecondMergeLists->next != NULL)
                        HeadOfSecondMergeLists = HeadOfSecondMergeLists->next;
                    else
                        FlagHaveSecondHalf = false;
                }
                if (FlagHaveSecondHalf){                                          //if we have list with length = 17, n = 8. The 2-nd 
                buff = HeadOfSecondMergeLists;                                    //piece have length = 1, haven't 2-nd half.
                HeadOfSecondMergeLists = HeadOfSecondMergeLists->next;
                buff->next = NULL;
                ListStart->next = NULL;
                ListStart->next = mergeTwoLists(HeadOfFirstMergeLists, HeadOfSecondMergeLists);               //merge it
                }
                while(ListStart->next != NULL)
                    ListStart = ListStart->next;
                ListStart->next = ListEnd;
                HeadOfFirstMergeLists = ListEnd;
                HeadOfSecondMergeLists = ListStart;
                
                    
            }
            n *= 2;
            ListHead = ListFalse->next;
        }
        delete(ListFalse);
        return ListHead;    
        
    }
};
```
