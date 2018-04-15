---
layout: post
#标题配置
title: "栈的实现"
#时间配置
date:   2018-04-15 19:09:01 +0800
#大类配置
categories: 数据结构
#小类配置
tag: 栈
---

* content
{:toc}
 

### 栈

=================================================  
**栈(stack)是一种比较常用的线性数据结构，函数的递归调用是用栈来操作的。  
栈的核心特点是先进后出，允许插入和删除那一端是栈顶，另一端是栈底。  
下面介绍的是顺序栈。**
 {% highlight ruby %}
struct Node;
typedef struct Node *PNode;
struct Node{
	DataType info;
	PNode link;
};
typedef struct LinkStack{
	PNode top;
}*PLinkStack; 
{% endhighlight %}

### 创建栈
包括创建和判空。  

 代码如下： 

 {% highlight ruby %}
 int isEmptyStack_link(PLinkStack plstack){
	return plstack -> top == NULL;
}
PLinkStack createEmptyLinkStack(){
	PLinkStack plstack;
	plstack = (PLinkStack)malloc(sizeof(struct LinkStack));
	if(plstack != NULL){
		plstack -> top = NULL;
	}else{
		cout << "Out of space!" << endl;
	}
	return plstack;
}
{% endhighlight %}

### 栈push

=================================================  

 <img src="{{  'http://oyku9aqxp.bkt.clouddn.com/stackpush.gif'| prepend: site.baseurl }}"  width="777" align="middle"/>   

伪代码如下： 

 {% highlight ruby %}
void push_link(PLinkStack plstack, DataType x){
	PNode p;
	p = (PNode)malloc(sizeof(struct Node));
	if(p == NULL){
		cout << "Out of space!" << endl;
	}else{
		p -> info = x;
		p -> link = plstack -> top;
		plstack -> top = p;
	}
}
{% endhighlight %}

### 栈pop

=================================================  



 <img src="{{  'http://oyku9aqxp.bkt.clouddn.com/stackpop.gif'| prepend: site.baseurl }}"  width="777" align="middle"/>   

伪代码如下：  

  {% highlight ruby %}
int pop_link(PLinkStack plstack){
	PNode p;
	if(isEmptyStack_link(plstack)){
		cout << endl << "Underflow!" << endl;
		return 0;
	}else{
		DataType temp;
		p = plstack -> top;
		temp = p -> info;
		plstack -> top = plstack -> top -> link;
		free(p);
		return temp;
	}
}
{% endhighlight %}  
 **按老师要求改成return int，使用更方便(在后续的问题中)。  
 但是有bug，不严密。还是返回void比较好。**

### 完整代码

=================================================  
  

  {% highlight ruby %}
#include <bits/stdc++.h>
#define DataType int
using namespace  std;
int op;
DataType data;
struct Node;
typedef struct Node *PNode;
struct Node{
	DataType info;
	PNode link;
};
typedef struct LinkStack{
	PNode top;
}*PLinkStack; 

PLinkStack createEmptyLinkStack(){
	PLinkStack plstack;
	plstack = (PLinkStack)malloc(sizeof(struct LinkStack));
	if(plstack != NULL){
		plstack -> top = NULL;
	}else{
		cout << "Out of space!" << endl;
	}
	return plstack;
}
int isEmptyStack_link(PLinkStack plstack){
	return plstack -> top == NULL;
}
void push_link(PLinkStack plstack, DataType x){
	PNode p;
	p = (PNode)malloc(sizeof(struct Node));
	if(p == NULL){
		cout << "Out of space!" << endl;
	}else{
		p -> info = x;
		p -> link = plstack -> top;
		plstack -> top = p;
	}
}
int pop_link(PLinkStack plstack){
	PNode p;
	if(isEmptyStack_link(plstack)){
		cout << endl << "Underflow!" << endl;
		return 0;
	}else{
		DataType temp;

		p = plstack -> top;
		temp = p -> info;
		plstack -> top = plstack -> top -> link;
		free(p);
		return temp;
	}
}
void Done(){
	cout << endl << "Done!" << endl << endl;;
}
void LinkStack_Menu(){
	cout << "1.Create" << endl;
	cout << "2.Push" << endl;
	cout << "3.Pop" << endl;
	cout << "0.Exit" << endl;
	cout << "Please choose your operation:(1, 2, 3, 0)" << endl;
}
void linkstack(){
	PLinkStack plstack;
	while(1){
		LinkStack_Menu();
		cin >> op;
		switch(op){
			case 1:
				plstack = createEmptyLinkStack();
				Done();
				break;
			case 2:
				cout << "Please input the element:" << endl;
				cin >> data;
				push_link(plstack, data);
				Done();
				break;
			case 3:
				cout << endl << "The element is:" << pop_link(plstack);
				Done();
				break;
			case 0:
				return;
		}
	}
}
int main(){
	linkstack();
}
{% endhighlight %}  
