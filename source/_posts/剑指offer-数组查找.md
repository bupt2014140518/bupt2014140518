title: 剑指offer-数组查找
date: 2015-10-07 20:28:31
tags: 剑指offer
categories: 题库
---
主要是运用c++ vector实现二维数组查找~
![Italy](http://7xn88r.com1.z0.glb.clouddn.com/Tuscany,%20Italy6.jpg)
<!--more-->
### 问题描述
在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
### 代码
```cpp
#include <iostream>
#include <vector>
using namespace std;
bool findItem_quick(vector<vector<int>> array,int target)//从每行的最右边开始，减少比较次数
{
	if (array.empty())
	{
		return	false;
	}
	int row = array.size();
	int col = array[0].size();
	int i=0, j=col-1;
	while (i<row && j>=0)
	{
		if (array[i][j] == target)
		{
			return true;
		}
		else if (array[i][j] > target)
		{
			j--;
		}
		else if (array[i][j] < target)
		{
			i++;
		}
	}
	return false;
}
bool findItem(vector<vector<int>> array, int target)//中规中矩
{
	if (array.empty())
	{
		return	false;
	}
	int row = array.size();
	int col = array[0].size();
	for (int i = 0; i < row; i++)
	{
		for (int j = 0; j < col; j++)
		{
			if (array[i][j] == target)
			{
				return true;
			}
		}
	}
	return false;
}
void main()
{
	int a[2][4] = { { 1,2,3,4 },{ 5,6,7,8 } };
	vector< vector<int>> ver(2,vector<int>(4));//vector初始化
	for (int i = 0; i < 2;i++) 
	{
		for (int j = 0; j < 4; j++)
		{
			ver[i][j] = a[i][j];
		}
	}
	int target = 4;
	bool is_existed = findItem_quick(ver,target);
//	bool is_existed = findItem(ver,target);
	cout << is_existed << endl;
	system("Pause");
}
```