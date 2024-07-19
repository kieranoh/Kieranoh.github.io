---
layout: single
title:  "Bubble Sort"
categories: DataStructure
tag: [DataStructure, Sorting, Bubble-Sort]
toc: true
author_profile: false
---

# Bubble Sort

이번 목표는 Sorting 기법중 하나인 Bubble Sort를 C언어로 구현하는것이다.

Bubble Sort (버블 정렬)은 인접한 두 원소를 검사하여 정렬하는 알고리즘이다

시간 복잡도 O(n^2)

공간복잡도 O(n)

## 설명

버블 정렬은 첫번째 자료와 두번째 자료를 비교, 두번째 자료와 세번째 자료 비교,... 마지막-1 자료와 마지막 자료를 비교하여정렬한다.

이를 한번 마지막까지 실행하면 가장 큰 자료가 맨 뒤로 이동한다. 두번째 실행에서는 마지막을 제외하고 실행하면 정렬되는 데이터가 하나는 증가한다.


## 구현

```c
#include <stdio.h>

void bubbleSort(int arr[],int size)
{
	int temp;
	for(int i=0;i<size;i++)
	    {
	        for(int j=1;j<size-i;j++)
	        {
	            if(arr[j-1] > arr[j])
	            {
	                temp = arr[j-1];
	                arr[j-1] = arr[j];
	                arr[j] = temp;
	            }
	        }
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

	printf("before bubble sort\n");

	for(i = 0 ; i < cnt; i++)
	{
		printf("%d ",arr[i]);
	}
	printf("\nafter bubble sort\n");
    
	bubbleSort(arr,cnt - 1);    
	
    for(i = 0; i < cnt; i++)
	{
		printf("%d ", arr[i]);
	}
}

```

결과
```
before bubble sort
5  7  6  8  9  1  3  2  4  10
after bubble sort
1  2  3  4  5  6  7  8  9  10
```