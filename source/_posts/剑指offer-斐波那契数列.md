title: 剑指offer-斐波那契数列
date: 2015-10-10 19:20:15
tags: 剑指offer
categories: 题库
---
借助斐波那契数列来比较递归和动态规划，该题看似很适合斐波那契数列，但递归会造成栈溢出，用动态规划（循环）会好点~
![Horseshoe](http://7xn88r.com1.z0.glb.clouddn.com/Horseshoe%20Bend,%20U.S..jpg)
<!--more-->
### 问题描述：
大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项，有时间和内存限制。（注意：n从第0项开始的）
### 代码
```cpp
#include <iostream>
using namespace std;
int Fibonacci(int n) 
{
	int arr[2] = {0,1};
	if (n < 0)
	{
		return -1;
	}
	else if (n == 0) 
	{
		return 0;
	}
	else if (n == 1) 
	{
		return 1;
	}
	else
	{
		////递归(如果输入是个很大的n,是会溢出)
		//return Fibonacci(n-1) + Fibonacci(n-2);
		//循环(动态规划)
		int i = arr[0], j = arr[1],t;
		for (int k = 2; k <= n;k++)
		{
			t = i + j;
			i = j;
			j = t;
		}
		return t;
	}
}
int main() {
	// your code goes here
	int n;
	cin >> n;
	cout << Fibonacci(n) << endl;
	system("Pause");
	return 0;
}
```