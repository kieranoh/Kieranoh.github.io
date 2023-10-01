---
layout: single
title:  "Quick Sort"
categories: DataStructure
tag: [DataStructure, Sorting, Quick-Sort]
toc: true
author_profile: false
---

# Quick Sort

이번 목표는 Sorting 기법중 하나인 Quick Sort를 C언어로 구현하는것이다.

Quick Sort는 병합정렬과 비슷한 로직으로 기준이 되는 pivot을 기준으로 앞,뒤 배열을 쪼개어 기준값보다 작은 값을 앞으로, 큰값은 뒤로 보내어 재귀함수를 통해 정렬하는 방식이다.

시간 복잡도 O(nlongn)

공간복잡도 O(n)

## 설명

중간값을 pivot으로 설정을 한다면 왼쪽값을 left 오른쪽을 right로 설정한다. (L과 R은 index이다)

각각 반대 방향으로 이동하고, left는 기준보다 큰수, right는 기준보다 작은수를 만나면 멈추고 swap한다.

위 과정을 left가 right보다 오른쪽에 올 때까지 반복하고 반복한다.


## 구현

```c
#include <stdio.h>

void quick_sort(int *arr,int L,int R)
{
	int left = L;
	int right = R;
	int p = arr[(L+R)/2]; //pivot 설정 (가운데 기준값)
	int temp;//swap 용 temp

	do
	{
		while(arr[left]<p)
		{
			left++;
		}
		while(arr[right]>p)
		{
			right--;
		}
		if(left<=right)
		{
			temp = arr[left];
			arr[left] = arr[right];
			arr[right] = temp;
			left++;
			right--;			
		}
	}while(left<=right);
	
	if(L<right)
	{
		quick_sort(arr,L,right);
	}
	if(left<R)
	{
		quick_sort(arr,left,R);
	}
}

int main()
{
	int arr[10]={5,7,6,8,9,1,3,2,4,10};
	printf("before quick sort\n");
	for(int i = 0; i<10;i++)
	{
		printf("%d  ",arr[i]);
	}
	printf("\nafter quick sort\n");
	quick_sort(arr,0,10-1);
	for(int i = 0; i<10;i++)
	{
		printf("%d  ",arr[i]);
	}
	
	return 0;
}

```

결과
```
before quick sort
5  7  6  8  9  1  3  2  4  10
after quick sort
1  2  3  4  5  6  7  8  9  10
```