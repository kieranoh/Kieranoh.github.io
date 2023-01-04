---
layout: single
title:  "Linux Memory Layout"
categories: DreamHack
tag: [DreamHack, SystemHacking, Linux_Memory_Layout]
toc: true
author_profile: false
---

# Linux Memory Layout

[강의 주소](https://dreamhack.io/lecture/courses/52)

## 리눅스 프로세스의 메모리 구조

리눅스에서는 프로세스의 메모리를 크게 5가지 세그먼트(Segment)로 구분한다.

1. 코드 세그먼트
2. 데이터 세그먼트
3. BSS 세그먼트
4. 힙 세그먼트
5. 스택 세그먼트
   
운영체제가 메모리를 용도별로 나누면, 각 용도에 맞게 권한( <U>읽기</U> , <U>쓰기</U> , <U>실행</U> )을 부여할 수 있다는 장점이 있다.

![Segment](/images/segment.png)

### 코드 세그먼트
Code Segment (Text Segment)는 실행 가능한 기계코드가 위치하는 영역이다.

ex) main( )

프로그램이 동작하려면 실행 할 수 있어야 하므로  *읽기 권한* & *실행 권한* 이 부여된다. ( 쓰기 권한이 있으면 악의적으로 코드를 넣을 수 있으니 <U>쓰기 권한은 제거</U> )

### 데이터 세그먼트

Data segment는 컴파일 시점에서 값이 정해진 전역 변수 및 전역 상수들이 위치하는 영역이다.

데이터를 읽어야되기 때문에 *읽기 권한* 이 부여된다.

* 전역 변수 같이 값이 변할수 있는 데이터들은 *쓰기* 가능, Data Segment 라고 부른다.
* 전역 상수 같이 값이 변할 수 없는 데이터들은 *쓰기 불가능* , Rodata(REad-only_data) Segment라고 부른다.

ex)

```c
int data_num = 31337; // data

char data_rwstr[] = "writable_data"; // data

const char data_rostr[] = "readonly_data"; // rodata

char * str_ptr = "readonly" //str_ptr은 data, 문자열은 rodata

```

### BSS 세그먼트

BSS Segment( Block Started By Symbol Segment )는 컴파일 시점에서 값이 정해지지 않은 전역 변수가 위치하는 영역이다. ( 선언만 하고 초기화 하지 않은 변수들도 포함 )

프로그램이 시작될때 세그먼트 영역은 모두 0으로 값이 초기화 된다.

이 세그먼트에는 *읽기 권한* 및 *쓰기 권한* 이 부여된다.

ex)

아래 코드에서 초기화되지 않은 전역 변수인 bss_data가 BSS세그먼트에 위치하게 된다.

```c
int bss_data;

int main()
{
    printf("%d\n",bss_data); //0
    return 0;
}
```

### 스택 세그먼트

Stack Segment는 프로세스의 스택이 위치하는 영역이다. 함수의 인자나 지역변수와 같은 <U>임시</U> 변수들이 실행중 위치한다.

스택 세그먼트는 스택 프레임( Stack Frame )이라는 단위를 사용한다. 스택 프레임은 함수가 호출될 때 생성되고, 반환될 때 해제된다. ( 얼마나 필요한지는 값에 따라 달라져서 정확한 계산이 불가 )

운영체제는 프로세스가 시작할 때 작은 크기의 스택 세그먼트를 먼저 할당하고 부족할때 마다 확장한다. 스택은 <U>아래로 자란다</U> 라는 표현을 사용한다 ( 확장할 때 낮은 주소로 확장된다 )

이영역은 CPU가 자유롭게 값을 읽고 써야되서 *읽기 권한* 및 *쓰기 권한* 이 부여된다.

ex)

아래에 코드에서는 지역변수 choice가 스택에 저장된다.

```c
void func()
{
    int choice = 0;

    scanf("%d",&choice);

    if (choice)
    {
        call_true();
    }
    else
    {
        call_false();
    }

    return 0;
}

```

### 힙 세그먼트

Heap Segment는 힙데이터가 위치하는 영역이다. 스택과 같이 실행중 동적으로 할당될 수 있으며, 리눅스에서는 스택 세그먼트와 반대 방향으로 자란다. ( 충동을 피하기 위함 )

C언어에서 *malloc(), calloc()* 등 동적으로 할당 받는 메모리가 이 세그먼트에 위치한다.

스택 세그먼트와 같이 *읽기 권한* 및 *쓰기 권한* 이 부여된다.

ex)

```c
int main()
{
    int *heap_data_ptr = malloc(sizeof(*heap_data_ptr));
    // 동적 할당한 힙 영역의 주소를 가리킴

    *heap_data_ptr = 31337
    // 힙 영역에 값을 씀

    printf("%d\n",*heap_data_ptr);
    // 힙 영역의 값을 사용함

    return 0;
 }
```


## 요약


|세그먼트|역할|일반적인 권한|사용 예|
|---|---|---|---|
|코드 세그먼트|실행가능한 코드가 저장된 영역|읽기, 실행|main()등의 함수 코드|
|데이터 세그먼트| 초기화된 전역변수 또는 상수가 위치하는 영역| 읽기 와 쓰기 or 읽기 전용| 초기화된 전역변수, 전역 상수|
|BSS 세그먼트|초기화되지 않은 데이터가 위치하는 영역|읽기, 쓰기|초기화가 되지않은 전역변수|
|스택 세그먼트|임시 변수가 저장되는 영역|읽기, 쓰기|지역변수, 함수의 인자등|
|힙세그먼트| 실행중에 동적으로 사용되는 영역|읽기, 쓰기|malloc(),calloc()등으로 할당받은 메모리|