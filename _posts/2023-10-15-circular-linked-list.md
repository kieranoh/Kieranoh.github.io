---
layout: single
title:  "Circular Linked List"
categories: DataStructure
tag: [DataStructure, List, Circular_Linked_list]
toc: true
author_profile: false
---

# Circular Linked List

이번 목표는 자료구조중 하나인 Circular Loinked List, 원형 연결 리스트를 c 언어로 구현하는것 이다. 원형 연결 리스트는 노드를 이용해서 리스트를 만드는 것이다

## 구조

Node ->Node *next, int data

List ->Node *head(시작),Node *tail(마지막),Node *cur(현재),Node *before(현재 -1)

brfore를 사용하는 이유는 remove를 하기위해 사용된다.


remove 함수는 li->before->next 주소를(리스트의 현재 위치 -1 의 next 주소) li->cur-> next 주소로 (리스트 현재 위치의 다음주소) 바꾸어 주고, li->cur를 (리스트의 현재 위치) li->before로 (리스트의 현재 위치 -1) 바꾸어준후 free를 통해 제거해준다.



## 구현

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Node{
	struct Node *next;
	int data;
}Node;

typedef struct List{
	Node *head;
	Node *tail;
	Node *cur;
	Node *brefore;
}List;

void init(List *li)
{
	li->head = NULL;
	li->tail = NULL;
	li->cur = NULL;
	li->brefore = NULL;
	
}

void Insert_node(List *li, int num)
{
	Node *temp = (Node*)malloc(sizeof(Node));
	temp->data = num;
	
	if(li->head == NULL)
	{
		li->head = temp;
		li->tail = temp;
		temp->next = temp;
	}
	else
	{
		temp->next = li->tail->next;
		li->tail->next = temp;
		li->tail = temp;	
	}
}

void Cur_init(List *li)
{
	li->cur = li->tail;
	li->brefore = li->tail;
}

void Remove_node(List *li)
{
	Node *temp = li->cur;
	if(temp == li->tail)
	{
		if(li->tail == li->tail->next)
		{
			li->head = NULL;
			li->tail = NULL;
		}
		else
		{
			li->tail = li->brefore;
		}
	}
	li->brefore->next = li->cur->next;
	li->cur = li->brefore;
	free(temp);
}


int main()
{
	int num;
	scanf("%d",&num;
	
	List li;
	init(&li);
	
	for(int i = 1;i<=num;i++)
	{
		Insert_node(&li,i);
	}
	
	Cur_init(&li);
	
	return 0;
}

```
 
