title: 剑指offer-数组重整
date: 2015-10-12 19:47:50
tags: 剑指offer
categories: 题库
---
考查：代码的完整性，主要用于快排，插排的思想解决实际问题~
![Salar](http://7xn88r.com1.z0.glb.clouddn.com/Salar%20de%20Uyuni,%20Bolivia2.jpg)
<!--more-->
### 问题描述
输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于位于数组的后半部分，
并保证奇数和奇数，偶数和偶数之间的相对位置不变。
***主要有三种思路***
1. 插排的思路
2. 快排的思路（不保证奇数与奇数的顺序）
3. 最简单的用数组复制的思路]

### 代码
**思路1 插排**
```cpp
void reOrderArray(vector<int> &array) {
        for(int i=0;i<array.length;i++){
            if(array[i]%2==1){
                int temp=array[i];
                int j=i-1;
                while(j>=0&&array[j]%2==0){
                    array[j+1]=array[j];
                    j--;
                }
                array[j+1]=temp;
            }            
        }
    }
```
**思路2 最简单的复制**
奇数在a数组，偶数在b数组，然后再讲array的数组重新插入a&b
**思路3 快排（无序）**
```cpp
  void reOrderArray(vector<int> &array) {
        int i=0;
        int j=array.length-1;
        while(i<j){
            while(i<j&&array[i]%2==1){
                i++;
            }
            while(i<j&&array[j]%2==0){
                j--;
            }
            int temp=array[j];
            array[j]=array[i];
            array[i]=temp;
        }
    }
```