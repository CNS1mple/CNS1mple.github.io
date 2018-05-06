---
layout: post
#标题配置
title: "秒杀快排的猴子排序（雾"
#时间配置
date:   2018-04-27 12:04:01 +0800
#大类配置
categories: 算法
#小类配置
tag: 排序
---

* content
{:toc}
 

### 无限猴子定理

=================================================  
  
  
  
  
        
**一只猴子随机敲打键盘，如果给定的时间无限，这只猴子可以敲打出任何内容**  

**比如《大英百科全书》** 

### 猴子排序  

=================================================  
  
  
  

如果数组未排好序，随机打乱数组，再判断是否排好序  

**传说中秒杀一众辣鸡排序最优时间复杂度为O(1)的排序(滑稽)**(其实是O(N)...)  

平均复杂度是O(N*N!)，最坏可以跑到世界尽头- -  

 {% highlight ruby %}
do{
	shuffle(s)
}while(!issorted(s));
{% endhighlight %}  



### 丑陋的代码

=================================================  
  

  {% highlight ruby %}
#include <bits/stdc++.h>
using namespace std;
int s[105], res[105];
int len;
bool sorted(){
	for(int i = 1; i < len; i++)
		if(res[i] < res[i-1]) return false;
	return true;
}

void shuffle(){
	int flag[105];
	int reslen = 0;
	memset(flag, 1, sizeof(flag));
	int temp = len;
	while(len){
		int t = rand() % temp;
		if(flag[t]){
			flag[t] = 0;
			len--;
			res[reslen++] = s[t];
		}
	}
	len = temp;
}
bool ssorted(){
	for(int i = 1; i < len; i++)
		if(s[i] < s[i-1]) return false;
	return true;
}
int main(){
	cin >> len;
	int cnt = 0;
	for(int i = 0; i < len; i++){
		cin >> s[i];
	}
	if(ssorted()){
		cout << "已经排好序。";
		return 0; 
	}
	do{
		shuffle();
		cnt++;
	}while(!sorted());
	cout << "运行次数：" << cnt << endl;
	for(int i = 0; i < len; i++){
		cout << res[i] << " ";
	} 
}

{% endhighlight %}  

### 结果

=================================================  


 <img src="{{  'http://oyku9aqxp.bkt.clouddn.com/MonkeySort.png'| prepend: site.baseurl }}"  width="777" align="middle"/>     

 对我等非洲人来说，真的是慢的可以-_-!!

