---
layout: single
title:  "Binary Search"
categories: DataStructure
tag: [DataStructure, Search, Binary-search]
toc: true
author_profile: false
---

# Binary Search

이번 목표는 탐색 기법중 하나인 Binary Search(이진 검색)를 C언어로 구현하는 것 이다.

이진 검색을 사용하기 위해 사용되는 배열은 정렬된 상태여야한다.

이 알고리즘은 반씩 나눠서 검색을 반복하는것이다

## 설명

중간 index인 mid 를 설정해주고, 찾고 싶은 값이 mid 보다 크면 mid+1와 가장 우측 값 사이에서 다시 반을 나누고, 작다면 가장 왼쪽 값과 mid 사이에서 반을 나눈다. 원하는 값이 나올때 까지 반복을 하고 왼쪽 index와 오른쪽 index가 같으면 탐색을 멈춘다


## 구현

```c
#include <stdio.h>

int binary_search(int *arr,int target, int size)
{
	if(arr[0]>target || arr[size-1] < target)
	{
		
		return -1;
	}
	// 최대 최소를 통해 미리 찾기
	
	int left = 0;
	int right = size-1;
	int mid;
	
	while(left<=right)
	{
		mid =(left+right)/2;
		if(arr[mid]==target)
		{
			return mid;
		}
		if(arr[mid]<target)
		{
			left = mid+1;
			//mid보다 크다면 우측 절반을 다시 찾기
		}
		else
		{
			right = mid-1;
		}
	}
	
}

int main()
{
	int arr[6] = {2,4,6,10,45,95};
	
	printf("array is \n");
	for(int i = 0;i<6;i++)
	{
		printf("%d  ",arr[i]);
	}
	printf("\n");
	
	int target = 6;
	int result = binary_search(arr,target,6);
	printf("target is %d ,it is in %d\n",target,result);
	
	target = 1;
	result = binary_search(arr,target,6);
	printf("target is %d ,it is in %d\n",target,result);
	
	result = binary_search(arr,target,6);
	target = 13;
	printf("target is %d ,it is in %d\n",target,result);
	
	return 0;
	
}

```

결과
```
array is
2  4  6  10  45  95
target is 6 ,it is in 2
target is 1 ,it is in -1
target is 13 ,it is in -1
```