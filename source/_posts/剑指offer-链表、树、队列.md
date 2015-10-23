title: 剑指offer-链表、树、队列
date: 2015-10-07 20:30:20
tags: 剑指offer
categories: 题库
---
输入一个链表，从尾到头打印链表每个节点的值。
![Greece](http://7xn88r.com1.z0.glb.clouddn.com/Santorini,%20Greece.jpg)
<!--more-->
### 问题描述-链表
输入一个链表，从尾到头打印链表每个节点的值。
### 代码
```cpp
struct ListNode {
        int val;
        struct ListNode *next;
        ListNode(int x) :
              val(x), next(NULL) {
        }
  };
class Solution {
public:
    vector<int> printListFromTailToHead(struct ListNode* head) {
        vector<int> v;
        while(head != NULL)
        {
            v.insert(v.begin(),head->val);//insert就是倒序插入，从前插入
            head = head->next;
        }
        //reverse(v.begin(),v.end());//适用于push_bach
        return v;
    }
};
```
### 问题描述-树
输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。
### 代码
```bash
#include <iostream>
#include <vector>
using namespace std;
//Definition for binary tree
struct TreeNode {
	int val;
	TreeNode *left;
	TreeNode *right;
	TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
class Solution {
public:
	struct TreeNode* reConstructBinaryTree(vector<int> pre, vector<int> in) {
		int inCount = in.size();
		if (inCount == 0)
			return NULL;
		vector<int> left_pre, right_pre, left_in, right_in;
		//创建根节点，根节点肯定是前序遍历的第一个数
		TreeNode* Head = new TreeNode(pre[0]);
		//找到中序遍历根节点所在位置,存放于变量root中
		int root = 0;
		for (int i = 0; i<inCount; i++)
		{
			if (in[i] == pre[0])
			{
				root = i;
				break;
			}
		}
		//对于中序遍历，根节点左边的节点位于二叉树的左边，根节点右边的节点位于二叉树的右边
		//利用上述这点，对二叉树节点进行归并
		for (int i = 0; i<root; i++)
		{
			left_in.push_back(in[i]);
			left_pre.push_back(pre[i + 1]);//前序第一个为根节点
		}
		for (int i = root + 1; i<inCount; i++)
		{
			right_in.push_back(in[i]);
			right_pre.push_back(pre[i]);
		}
		//和shell排序的思想类似，取出前序和中序遍历根节点左边和右边的子树
		//递归，再对其进行上述所有步骤，即再区分子树的左、右子子数，直到叶节点
		Head->left = reConstructBinaryTree(left_pre, left_in);
		Head->right = reConstructBinaryTree(right_pre, right_in);
		return Head;
	}
	struct TreeNode* reConstructBinaryTree2(vector<int> in, vector<int> post) {
		int inCount = in.size();
		if (inCount == 0)
			return NULL;
		vector<int> left_post, right_post, left_in, right_in;
		//创建根节点，根节点肯定是后序遍历的最后一个数
		TreeNode* Head = new TreeNode(post[inCount-1]);
		//找到中序遍历根节点所在位置,存放于变量root中
		int root = 0;
		for (int i = 0; i < inCount; i++)
		{
			if (in[i] == post[inCount - 1])
			{
				root = i;
				break;
			}
		}
		//对于中序遍历，根节点左边的节点位于二叉树的左边，根节点右边的节点位于二叉树的右边
		//利用上述这点，对二叉树节点进行归并
		for (int i = 0; i < root; i++)
		{
			left_in.push_back(in[i]);
			left_post.push_back(post[i]);//前序第一个为根节点
		}
		for (int i = root + 1; i < inCount; i++)
		{
			right_in.push_back(in[i]);
			right_post.push_back(post[i-1]);
		}
		//和shell排序的思想类似，取出后序和中序遍历根节点左边和右边的子树
		//递归，再对其进行上述所有步骤，即再区分子树的左、右子子数，直到叶节点
		Head->left = reConstructBinaryTree2(left_in,left_post);
		Head->right = reConstructBinaryTree2(right_in,right_post);
		return Head;
	}
	//由树得到后序遍历
	void getPostTraverse(TreeNode * node)
	{
		if (node) {
			getPostTraverse(node->left);
			getPostTraverse(node->right);
			cout << node->val << " ";
		}
	}
	//由树得到中序遍历
	void getInTraverse(TreeNode * node)
	{
		if (node) {
			getInTraverse(node->left);
			cout << node->val << " ";
			getInTraverse(node->right);
		}
	}
	//由树得到前序遍历
	void getPreTraverse(TreeNode * node)
	{
		if (node) {
			cout << node->val << " ";
			getPreTraverse(node->left);
			getPreTraverse(node->right);
		}
	}
};
void main()
{
	vector<int> vv1,vv2;
	int i=0,j=0;
	char a;
	while (cin>>i)
	{
		vv1.push_back(i);
		a= cin.get();
		if (a == '\n')
			break;
	}
	while (cin >> j)
	{
		vv2.push_back(j);
		a = cin.get();
		if (a == '\n')
			break;
	}
	Solution ss;
	//TreeNode *tt = ss.reConstructBinaryTree(vv1,vv2);
	//ss.getPostTraverse(tt);
	//cout << endl;
	//ss.getPreTraverse(tt);
	//cout << endl;
	//ss.getInTraverse(tt);
	//cout << endl;
	TreeNode *tt2 = ss.reConstructBinaryTree2(vv1, vv2);
	ss.getPreTraverse(tt2);
	cout << endl;
	system("Pause");

}
```
#### Note
（1）可以由前序、中序和中序、后序，求出第三种序列；但是前序和后序不可以；
（2）前序第一个是root节点，中序找到root所在位置，左是root的左子树组，右是右子树组；同理，后序最后一个是root节点，剩下的和前面类似，递归最终求出第三种序列。
### 问题描述-对列
用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。
### 代码
```bash
class Solution
{
public:
    void push(int node) {
        stack1.push(node);
    }

    int pop() {
        if(stack2.empty())
        {
            if(stack1.empty())
            {
                cout << "List is empty" << endl;
                return -1;
            }
            else{
                while(!stack1.empty())
                {
                   stack2.push(stack1.top());
                   stack1.pop();
                }
            }       
        }
        int a = stack2.top();
        stack2.pop();
        return a;
    }

private:
    stack<int> stack1;
    stack<int> stack2;
};
```
#### Note
（1）栈是先进后出；队列是先进先出。