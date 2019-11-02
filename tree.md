# LeetCode_TREE

+ [Binary Tree Inorder Traversal](#binary-tree-inorder-traversal)
+ [Symmetric Tree](#symmetric-tree)
+ [Maximum Depth of Binary Tree](#maximum-depth-of-binary-tree)
+ [Same Tree](#same-tree)
+ [Invert Binary Tree](#invert-binary-tree)
+ [Path Sum](#path-sum)
+ [Binary Tree Level Order Traversal](#binary-tree-level-order-traversal)
+ [Subtree of Another Tree](#subtree-of-another-tree)
+ [Kth Smallest Element in a BST](#kth-smallest-element-in-a-bst)
+ [Lowest Common Ancestor of a Binary Tree](#lowest-common-ancestor-of-a-binary-tree)
+ [Lowest Common Ancestor of a Binary Search Tree](#lowest-common-ancestor-of-a-binary-search-tree)
+ [Validate Binary Search Tree](#validate-binary-search-tree)
+ [Binary Search Tree Iterator](#binary-search-tree-iterator)
+ [12](#12)



## Definition for a binary tree node

```C++
struct TreeNode {
      int val;
      TreeNode *left;
      TreeNode *right;
      TreeNode(int x) : val(x), left(NULL), right(NULL) {}
  };


```

## Binary Tree Inorder Traversal

https://leetcode.com/problems/binary-tree-inorder-traversal/

```C++
void Answer(TreeNode* root, vector<int>& answer){
    if(root != NULL){
        Answer(root->left, answer);
        answer.push_back(root->val);
        Answer(root->right, answer);
    }
}
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> answer;
        Answer(root, answer);
        return answer;
    }
};
```

## Symmetric Tree

https://leetcode.com/problems/symmetric-tree/

```C++
bool Answer(TreeNode* rLeft, TreeNode* rRight){
    if ((rLeft == NULL)&&(rRight == NULL))
        return true;
    if ((rLeft == NULL)||(rRight == NULL))
        return false;
    return (rRight->val == rLeft->val)
         &&(Answer(rLeft->left, rRight->right))
         &&(Answer(rLeft->right, rRight->left));
}

class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(root == NULL)
            return true;
        return Answer(root->left, root->right);        
    }
};
```

## Maximum Depth of Binary Tree

https://leetcode.com/problems/maximum-depth-of-binary-tree/

```C++
class Solution {
public:
    int maxDepth(TreeNode* root) {
      if(root != NULL){
        return max(maxDepth(root->left), maxDepth(root->right)) + 1;
      }
      return 0;
    }
};
```

## Same Tree

https://leetcode.com/problems/same-tree/

```C++
bool Answer(TreeNode* root1, TreeNode* root2){
    if ((root1 == NULL)&&(root2 == NULL))
        return true;
    if ((root1 == NULL)||(root2 == NULL))
        return false;
    return (root2->val == root1->val)
         &&(Answer(root1->left, root2->left))
         &&(Answer(root1->right, root2->right));

}
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        return Answer(p, q);    
    }
};
```

##  Invert Binary Tree

https://leetcode.com/problems/invert-binary-tree/

```C++
void Answer(TreeNode* root){
    if(root != NULL){
        Answer(root->left);
        Answer(root->right);
        TreeNode* buf = root->left;
        root->left = root->right;
        root->right = buf;
    }
}
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        Answer(root);
        return root;
    }
};
```

## Path Sum

https://leetcode.com/problems/path-sum/

```C++
class Solution {
public:
    bool hasPathSum(TreeNode* root, int sum) {
      if(root == NULL)
        return false;
      if((root->left != NULL) ||(root->right != NULL))
        return (hasPathSum(root->left, sum - root->val))
             ||(hasPathSum(root->right, sum - root->val));
      return sum == root->val;
}
};
```

## Binary Tree Level Order Traversal

https://leetcode.com/problems/delete-node-in-a-linked-list/

```C++
void Answer(TreeNode* root, vector<vector<int>>& answer, int level){
    if(root != NULL){
        if(answer.size() < level + 1)
            answer.push_back(vector<int> {root->val});
        else
            answer[level].push_back(root->val);
        Answer(root->left, answer, level + 1);
        Answer(root->right, answer, level + 1);
    }
}
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> answer;
        Answer(root, answer, 0);
        return answer;
        
    }
};
```

## Subtree of Another Tree

https://leetcode.com/problems/subtree-of-another-tree/

```C++
bool Answer(TreeNode* root1, TreeNode* root2){
    if ((root1 == NULL)&&(root2 == NULL))
        return true;
    if ((root1 == NULL)||(root2 == NULL))
        return false;
    return (root2->val == root1->val)
         &&(Answer(root1->left, root2->left))
         &&(Answer(root1->right, root2->right));

}
bool SubAnswer(TreeNode* root1, TreeNode* root2){
    if(root1 != NULL){
        if (Answer(root1, root2))
            return true;
        return SubAnswer(root1->left, root2)||SubAnswer(root1->right, root2);
    }
    return false;
}
class Solution {
public:
    bool isSubtree(TreeNode* s, TreeNode* t) {
        return SubAnswer(s, t);
    }
};
```

## Kth Smallest Element in a BST

https://leetcode.com/problems/kth-smallest-element-in-a-bst/

```C++
int Answer(TreeNode* root, int& k){
    int sum1 = 0, sum2 = 0;
    if(root != NULL){
        sum1 = Answer(root->left, k);
        k--;
        if (k == 0)
            return root->val;
        sum2 = Answer(root->right, k);
        return sum1 + sum2;
    }
    return 0;
}
class Solution {
public:
    int kthSmallest(TreeNode* root, int k) {
        return Answer(root, k);
    }
};
```

## Lowest Common Ancestor of a Binary Tree

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

```C++
TreeNode* Answer(TreeNode* root, TreeNode* p, TreeNode* q){
    TreeNode* TreeLeft = 0, *TreeRight = 0;
    if(root != NULL){
        TreeLeft = Answer(root->left, p, q);
        if((root == p)||(root == q))
            return root;
        TreeRight = Answer(root->right, p, q);
        if(TreeLeft == NULL)
            return TreeRight;
        if(TreeRight == NULL)
            return TreeLeft;
        return root;
    }
    return NULL;
}
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        return Answer(root, p, q);
    }
};
```

## Lowest Common Ancestor of a Binary Search Tree

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/

```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        int minTreeLeave = min(p->val, q->val), maxTreeLeave = max(p->val, q->val);
        while(root){
            if(root->val > maxTreeLeave)
                root = root->left;
            else
                if(root->val < minTreeLeave)
                    root = root->right;
                else
                    return root;
        }
    }
};
```

## Validate Binary Search Tree

https://leetcode.com/problems/validate-binary-search-tree/

### With additional memory(20.7 MB)
```C++
void Answer(TreeNode* root, vector<int>& answer){
    if(root != NULL){
        Answer(root->left, answer);
        answer.push_back(root->val);
        Answer(root->right, answer);
    }
}
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        vector<int> answer;
        int i = 0;
        Answer(root, answer);
        if (root == NULL)
            return true;
        for(i = 0; i < answer.size()-1;i++)
            if(answer[i] >= answer[i+1])
                return false;
        return true;
    }
};
```
### Without additional memory(20.4 MB)

```C++
bool Answer(TreeNode* root, long int down, long int up){
    bool bool1 = false, bool2 = false;
    if(root != NULL){
        bool1 = Answer(root->left, down, root->val);
        bool2 = Answer(root->right, root->val, up);
        if((down >= root->val)||(up <= root->val))
            return false;
        return bool1 && bool2;
    }
    return true;
}
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return Answer(root, -INFINITY, INFINITY);
    }
};
```
## Binary Search Tree Iterator

https://leetcode.com/problems/binary-search-tree-iterator/

```C++
class BSTIterator {
    vector<int> SortVector;
    int index = 0;
    void PutOrderIn(TreeNode* root) {
      if(root != NULL){
        PutOrderIn(root->left);
        SortVector.push_back(root->val);
        PutOrderIn(root->right);
      }
    }
public:   
    BSTIterator(TreeNode* root) {
      PutOrderIn(root);
    }
    int next() {
      return SortVector[index++];
    }
    bool hasNext() {
      return (index) < (SortVector.size());
    }
};
```
## Definition for a binary tree node for 12 

```C++
struct TreeNode {
TreeNode *parent;
TreeNode *left;
TreeNode *right;
};
```

## 12

```C++
TreeNode* Answer(TreeNode* node){
    TreeNode* result;
    if(node != NULL){
        if(node->right != NULL){
          result = node->right;
          while(result->left != NULL)
            result = result->left;
        }
        else{
          TreeNode* buf = node;
          result = node->parent;
          while((buf == result->right)&&(result != NULL)){
            buf = buf->parent;
            result = result->parent;
          }
        }
    }
    return result;
}
TreeNode* inorderSuccessor(TreeNode* node) {
    return Answer(node);
};
```
