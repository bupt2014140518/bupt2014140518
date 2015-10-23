title: 剑指offer-字符串替换与常规问题
date: 2015-10-07 20:25:12
tags: 剑指offer
categories: 题库
---
主要是考查char的使用，注意指针、变量等的区别联系~
![Italy](http://7xn88r.com1.z0.glb.clouddn.com/Tuscany-Italy.jpg)
<!--more-->
### 问题描述
请实现一个函数，将一个字符串中的空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。
### 代码
```bash
#include <iostream>
#include <string>
using namespace std;
void replaceSpace(char *str, int length)
{
	int i = 0, j = length;
	for (i = 0; i < length; i++) {
		if (str[i] == ' ')
			j += 2;
	}
	for (i = length - 1; i >= 0; i--) {
		if (str[i] == ' ') {
			str[--j] = '0';
			str[--j] = '2';
			str[--j] = '%';
		}
		else {
			str[--j] = str[i];
		}
	}
}

void main()
{
	char test[30] = "We are Happy"; //这里之所以写30，是因为替换之后，长度会扩展，避免溢出，需要长度够长，
	//如果不是这样，估计只能用string返回的方式
    replaceSpace(test, strlen(test));
	cout << test << endl;
	char *test30 = "We are Happy";
	string aa = "We are Happy";
	char *test2 = new char[10];
	char test10[] = "We are Happy";
	cout << "test[30]: " << sizeof(test) << endl;//输出30
	cout << "test[30]: " << strlen(test) << endl;//输出12
	cout << "test[]: " << sizeof(test10) << endl;//输出13
	cout << "test[]: " << strlen(test10) << endl;//输出12
	cout << "*test: " << sizeof(test30) << endl;//输出4
	cout << "*test: " << strlen(test30) << endl;//输出12
	cout << "test string: " << aa.length()<< endl; //输出12
	cout << "test string: " << sizeof(aa) << endl; //输出28，无意义
	cout << "*test=[]: " << sizeof(test2) << endl;//输出4
	cout << "*test=[]: " << strlen(test2) << endl;//输出22，无意义
	
	system("Pause");

}
```
### 小结

（1）此题需注意char单字符用‘’表示，不能用“”；
（2）char长度扩展，需要支持，避免越界，当然用string.apend或者pushback同样可以解决问题；
（3）关于sizeof、strlen、length()需要弄清楚使用的场景。