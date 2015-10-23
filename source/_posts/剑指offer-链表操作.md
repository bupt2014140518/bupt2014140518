title: 剑指offer-链表操作
date: 2015-10-13 19:06:35
tags: 剑指offer
categories: 题库
---
主要针对链表的操作~
![Grand Teton](http://7xn88r.com1.z0.glb.clouddn.com/Grand%20Teton%20National%20Park,%20U.S..jpg)
<!--more-->
### 问题描述1
输入一个链表，输出该链表中倒数第k个结点。
***分析1***
1. 最优：设定两个指针，让第一个指针和第二个指针都指向头结点，然后再让第一个指针走(k-1)步，到达第k个节点。
然后两个指针同时往后移动，当第一个结点到达末尾的时候，第二个结点所在位置就是倒数第k个节点了；
2. 较简单：首先算出链表的总长度n，然后返回第n-k个。

### 代码1
***思路11***
```cpp
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        if(head==null||k<=0){
            return null;
        }
        ListNode pre=head;
        ListNode last=head;       
        for(int i=1;i<k;i++){
            if(pre.next!=null){
                pre=pre.next;
            }else{
                return null;
            }
        }
        while(pre.next!=null){
            pre = pre.next;
            last=last.next;
        }
        return last;
    }
}
```
***思路12***
```cpp
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}
class Solution {
public:
    ListNode* FindKthToTail(ListNode* pListHead, unsigned int k) {
        ListNode* pp = pListHead;
        int n = 0;
        while(pp != NULL) {
            n++;
            pp = pp->next;
        }
        if(n < k or k==0 or pp==NULL) return NULL;
        int i = 0;
        pp = pListHead;
        while(pp != NULL && ++i < (n-k+1)) pp = pp->next;
        return pp;
    }
};
```
### 问题2
输入一个链表，反转链表后，输出链表的所有元素。
***头插法（三个指针轮换）***

### 代码2
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
    ListNode* ReverseList(ListNode* pHead) {
        ListNode* h = NULL;
		if(pHead){
			return NULL;
		}
        for(ListNode* p = pHead; p; ){
            ListNode* tmp = p -> next;
            p -> next = h;
            h = p;
            p = tmp;
        }
        return h;
    }
};
```
### 问题3
输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。
***注意tmp的作用***

### 代码3
***非递归方法***
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
    ListNode* Merge(ListNode* pHead1, ListNode* pHead2)
    {
         ListNode tmp(20), *p = &tmp;
        while(pHead1 || pHead2){
            if(!pHead2 || (pHead1 && pHead1 -> val <= pHead2 -> val)){
                p -> next = pHead1;
                pHead1 = pHead1 -> next;
            }
            else{
                p -> next = pHead2;
                pHead2 = pHead2 -> next;
            }
            p = p -> next;
        }
        return tmp.next;
    }
   
};
```
***递归方法***
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
    ListNode* Merge(ListNode* pHead1, ListNode* pHead2)
    {
        if(list1==null)
			return list2;
		else if(list2==null)
			return list1;
		ListNode mergeHead=null;
		if(list1.val<list2.val){
			mergeHead=list1;
			mergeHead.next=Merge(list1.next, list2);
		}
		else{
			mergeHead=list2;
			mergeHead.next=Merge(list1, list2.next);
		}
		return mergeHead;
	}
};
```