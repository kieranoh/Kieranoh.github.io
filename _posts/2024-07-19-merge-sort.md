---
layout: single
title:  "Merge Sort"
categories: DataStructure
tag: [DataStructure, Sorting, Merge-Sort]
toc: true
author_profile: false
---

# Merge Sort

이번 목표는 Sorting 기법중 하나인 Merge Sort를 C언어로 구현하는것이다.

Merge Sort(병합 정렬)은 하나의 리스트를 균등한 크기로 분할하고 분할한 리스트를 정렬한 다음 두개의 리스트를 다시 합하여 전체가 정렬되게 하는 것이다.

시간 복잡도 O(nlongn)

공간복잡도 O(n)

## 설명

Merge Sort는 총 3단계로 구성되어있다.

- 분할(Divide): 입력 배열을 같은 크기의 2개의 배열로 분할한다.
  
- 정복(Conquer): 각각 배열을 정렬한다.

- 결합(Combine): 정렬된 배열을 하나의 배열에 결합한다.

위 3단계를 수행하기 위해서 추가적인 리스트가 필요하다.


## 구현

```c
#include <stdio.h>

void merge(int a[], int low, int mid, int hight)   
{
	int b[100];
	int i = low;        
	int j = mid + 1;    
	int k = 0;          
	
	while(i <= mid && j <= hight)
	{
		if(a[i] <= a[j])        
			b[k++] = a[i++];
		else
			b[k++] = a[j++];
	}
	while(i <= mid)            
		b[k++] = a[i++];
	while(j <= hight)           
		b[k++] = a[j++];
	k--;
    
	while(k >= 0)               
	{
		a[low + k] = b[k];
		k--;
	}
}
void mergeSort(int a[], int low, int hight)    
{
	
	int mid;
	if(low < hight)
	{
		mid = (low + hight) / 2;
		mergeSort(a, low, mid);            
		mergeSort(a, mid + 1, hight);      
		merge(a, low, mid, hight);          
	}
}
int main(void)
{
	int arr[100];
	int i, cnt;        
	
	scanf("%d", &cnt);
	
	for(i = 0 ; i < cnt; i++)
	{
		scanf("%d", &arr[i]);
	}

	printf("before merge sort\n");

	for(i = 0 ; i < cnt; i++)
	{
		printf("%d ",arr[i]);
	}
	printf("\nafter merge sort\n");
    
	mergeSort(arr, 0, cnt - 1);    
	
    for(i = 0; i < cnt; i++)
	{
		printf("%d ", arr[i]);
	}
}

```

결과
```
before merge sort
5  7  6  8  9  1  3  2  4  10
after merge sort
1  2  3  4  5  6  7  8  9  10
```