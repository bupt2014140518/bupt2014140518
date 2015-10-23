title: 剑指offer-斐波那契数列应用-跳台阶&&矩形覆盖
date: 2015-10-10 20:39:11
tags: 剑指offer
categories: 题库
---
斐波那契数列的应用，递归和动态规划（循环）的灵活使用~
![Horseshoe](http://7xn88r.com1.z0.glb.clouddn.com/Horseshoe%20Bend,%20U.S1..jpg)
<!--more-->
### 问题描述：
一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法。
***分析***：
1.假设当有n个台阶时假设有f(n)种走法。
2.青蛙最后一步要么跨1个台阶要么跨2个台阶。
3.当最后一步跨1个台阶时即之前有n-1个台阶，根据1的假设即n-1个台阶有f(n-1)种走法。
4.当最后一步跨1个台阶时即之前有n-2个台阶，根据1的假设即n-2个台阶有f(n-2 )种走法。
5.显然n个台阶的走法等于前两种情况的走法之和即f(n)=f(n-1)+f(n-2)。
6.找出递推公式后要找公式出口，即当n为1、2时的情况，显然n=1时f(1)等于1，f(2)等于2。
### 代码
```cpp
//***递归法***
 int jumpFloor(int number) {
    int count = 0;
	if(number <= 0){
        return 0;
    }    
    else if(number == 1){
        return 1;
    }      
    else if(number == 2){
         return 2;
    }     
    else{
        count = jumpFloor(number-1) + jumpFloor(number-2);
        return count;
    }
}
//***动态规划法（循环）***
 int jumpFloor(int number) {
    if(number < 3) 
		returnnumber;    
	int two = 2;
	int one = 1;
	int result = 0;
	for(inti = 3; i <= number; ++i)
	{
		result = one + two;
		two = one;
		one = result;
		 
	} 
	return result;
}
//另外一种思路：***排列组合算法***
//问题解析：设共跳x个1级台阶，y个2级台阶，可推出x+2y=n => x=n-2y,
//最终问题为对n-2y个一级台阶与y个2级台阶排列组合，即C(n-y,y)。
//y的范围：y>=0&&y<=(n/2) x的范围：x>=0&&x<=0。
 //求排列组合数
 int com(int m,int n){  
    int i = m;  
    int j; 
    int sum=1; 
    for(j = 0;j < n;j++,i--){ 
        sum = sum *i / (j+1);  
    } 
    return sum;
 } 
 int jumpFloor(int number){ 
    int two; /*跳两级台阶的次数*/ 
    int count = 0; 
    for(two = 0;two<= (number/2);two ++){ 
        count += com(number-two,two);
    } 
    return count;
 } 
```
### 升级方式的跳台阶；
一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。
### 归纳分析
因为n级台阶，第一步有n种跳法：跳1级、跳2级、到跳n级
跳1级，剩下n-1级，则剩下跳法是f(n-1)
跳2级，剩下n-2级，则剩下跳法是f(n-2)
所以f(n)=f(n-1)+f(n-2)+...+f(1)
因为f(n-1)=f(n-2)+f(n-3)+...+f(1)
所以f(n)=2*f(n-1);
```cpp
 int jumpFloorII(int number) {
		if(number<=0){
            return 0;
        }
        else if(number==1){
            return 1;
        }
        else if(number>1){
            return 2*jumpFloorII(number-1);
        }
 }
  
```
### 另一应用——矩形覆盖
***题目描述***
我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？
```cpp
 int rectCover(int number) {
		if(number < 1){
           return 1; 
        }
        else if(number == 1 or number == 2){
            return number;
        }
        else{
            return rectCover(number-1)+rectCover(number-2);
        }
 }
```