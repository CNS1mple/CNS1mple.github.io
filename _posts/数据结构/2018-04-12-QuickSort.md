---
layout: post
#标题配置
title: "一种高效排序算法-快速排序及复杂度分析(含GIF图解"
#时间配置
date:   2018-04-12 16:02:01 +0800
#大类配置
categories: 数据结构
#小类配置
tag: 排序
---

* content
{:toc}
 




## QuickSort  

=================================================  


**快排是目前应用最广泛的算法。循环较小，不需要额外空间。思想比较简单：  
对unsorted的数列，设第一个元素为X，每次循环把X插到合法的位置。  
注意这个合法的位置，是指它前面的所有元素比它小，后面的所有元素比它大。  
与插入排序不同的是，这个合法的位置是被unsorted包围的。**  


 <img src="{{  'http://oyku9aqxp.bkt.clouddn.com/QuickSort.gif'| prepend: site.baseurl }}"  width="777" align="middle"/>   

  
**GIF使用的是二分法的思想。  
需要注意的点  
黄色的是设置的X，变紫色是不满足比X小，也就是比X大的元素置紫，同理比X小的置绿。  
把单个sorted数列所有元素上色之后  
之后的那一步插入，才算是合法的位置，即置橙色。  
请看图多理解几遍。**


## 伪代码  
  
=================================================  


 {% highlight ruby %}
for each (unsorted) partition//这步暗示递归，当时没看出来。。。
set first element as pivot
  storeIndex = pivotIndex + 1//这个index控制紫色的第一个和绿的的最后一个的位置
  for i = pivotIndex + 1 to rightmostIndex
    if element[i] < element[pivot]//如果当前元素小于X，将当前元素置绿，并与第一个紫色换位置
      swap(i, storeIndex); storeIndex++
  swap(pivot, storeIndex - 1)//将X和最后一个绿色换位置
{% endhighlight %}
  
  
## 代码实现
  

=================================================  

 {% highlight ruby %}
#include <bits/stdc++.h>
using namespace std;// 7 3 1 8 6 0 5 4

void Swap(int A[], int i, int j){
		int temp = A[i];
		A[i] = A[j];
		A[j] = temp; 
}
void QuickSort(int A[], int l, int r){
	if(l > r){
		return;
	}
	int temp, index;
	for(int i = l; i < r; i++){
		temp = A[i];
		index = i + 1;
		for(int j = i+1; j <= r; j++){
			if(A[j] < temp){
				Swap(A, j, index);
				index++;
			}
		}
		Swap(A, i, index-1);
		QuickSort(A, l, index-2);
		QuickSort(A, index, r);
	}
} 

int main() {
	int n;
	int s[105];
	cin >> n;
	for(int i = 0; i < n; i++){
		cin >> s[i];
	}
	QuickSort(s, 0, n-1);
	for(int i = 0; i < n; i++){
		cout << s[i] << " ";
	}
	return 0;
}
}
{% endhighlight %}  


## 个人实现  


=================================================  
 {% highlight ruby %}
#include <bits/stdc++.h>
using namespace std;

void Swap(int A[], int i, int j){
		int temp = A[i];
		A[i] = A[j];
		A[j] = temp; 
}
void QuickSort(int A[], int n){
	int temp;
	for(int i = 0; i < n; i++){
		temp = A[i];
		for(int j = n-1; j > i; j--){
			if(A[j] < temp){
				Swap(A, j, i);
				for(;i < j; i++){
					if(A[i] > temp){
						Swap(A, i, j);
						break;
					}
				}
			}	
		}
	}
}
int main() {
	int n;
	int s[105];
	cin >> n;
	for(int i = 0; i < n; i++){
		cin >> s[i];
	}
	QuickSort(s, n);
	for(int i = 0; i < n; i++){
		cout << s[i] << " ";
	}
	return 0;
}
{% endhighlight %}  
  

  **这个是我在还没理解上图思想时自己写的快速排序。  
  隐约记得蓝桥杯有一年代码填空出的快速排序好像是这样做的。  
  算是非递归的一种实现，稍微比图上好理解一点。**  

## 时间复杂度  



=================================================  


**快排的worst case是O(n2),有时候会超时。  
但瑕不掩瑜，快排依然是应用最广泛的排序算法。
严格的数学证明在算法导论里有。  
这里只需记住平均复杂度为O(nlgn)就行。  
其实我也不会XD**
  
   <img src="{{  'http://oyku9aqxp.bkt.clouddn.com/QuickSortO.png'| prepend: site.baseurl }}"  width="666" align="middle"/>   