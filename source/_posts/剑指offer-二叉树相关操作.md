title: 剑指offer-二叉树相关操作
date: 2015-10-20 14:42:57
tags: 剑指offer
categories: 题库
---
主要是对于二叉树的操作：判断是否是子树；遍历等等；由于二叉树的特点，递归是普遍适用于解决树的几乎所有的问题~
![Paris](http://7xn88r.com1.z0.glb.clouddn.com/Paris,%20France4.jpg)
<!--more-->
### 问题描述1——子树判断
输入两颗二叉树A，B，判断B是不是A的子结构。
***递归***

### 代码1
```cpp?linenums
//树定义
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};
class Solution {
public:
    bool isSubtree(TreeNode* pRoot1, TreeNode* pRoot2){
        if(pRoot2 == NULL) return true;
        if(pRoot1 == NULL) return false;
        if(pRoot1->val == pRoot2->val)
            return isSubtree(pRoot1->left,pRoot2->left) && isSubtree(pRoot1->right,pRoot2->right);
        else
            return false;         
    }
     
public:
    bool HasSubtree(TreeNode* pRoot1, TreeNode* pRoot2)
    {
        if(pRoot1 == NULL || pRoot2 == NULL) return false;
        return isSubtree(pRoot1,pRoot2) || HasSubtree(pRoot1->left,pRoot2) || HasSubtree(pRoot1->right,pRoot2);
    }
};
```
### 问题描述2——树的镜像
操作给定的二叉树，将其变换为源二叉树的镜像。 
二叉树的镜像定义：
         源二叉树 
    	    8
    	   /  \\
    	  6   10
    	 / \  /  \\
    	5  7 9  11
    	镜像二叉树
    	    8
    	   /  \\
    	  10   6
    	 / \  / \\
    	11 9 7   5
### 代码2
```cpp?linenums
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};
class Solution {
public:
    void Mirror(TreeNode *pRoot) {
		if(pRoot){
            TreeNode *tmp = pRoot->left;
            pRoot->left = pRoot->right;
            pRoot->right= tmp;
            if(pRoot->right){
                 Mirror(pRoot->right);
            }
            if(pRoot->left){
                 Mirror(pRoot->left);
            }
        }
    }
};
```



