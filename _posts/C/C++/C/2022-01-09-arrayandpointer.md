---
title: "배열과 포인터의 차이(?)"

categories:
  - C
tags:
  - [Parsing, C, read]

toc: true
toc_sticky: true
---

# 배열과 포인터의 차이(?)


- 대부분의 경우엔 배열과 포인터는 동일하게 처리 가능
- 아닌 경우도 있다




# 포인터와 배열의 속도 차이


## [index] 계산

```c
#include <stdio.h>

int sum(int *num, int end)
{
	size_t index;
	int result = 0;

	for (index = 0; index < len, ++index) {
		result += num[index];
	}
	return (result);
}

int main(void)
{
	int a[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
	int result;

	result = sum(a, 10);

	printf("%d\n", result);

	return (0);
}
```


## \*temp++ 계산

```c
#include <stdio.h>

int sum(int *num, int *end)
{
	int *temp = num;
	int result = 0;

	while (temp < end) {
		result += *temp++;
	}
	return (result);
}

int main(void)
{
	int a[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
	int result;

	result = sum(a, a + 10);

	printf("%d\n", result);

	return (0);
}

```


## 위 두 코드를 봤을때 둘 중 빠른 코드는?


- 두 코드 중에서 빠른 코드는 아래 \*temp++; 코드 이다. 그 이유는?

  - 배열 [ ] 은 언제나 첫 주소를 가서 그 주소에서 +를 해서 요소의 위치까지 이동을 한다
  - 포인터 \*temp++ 는 이미 다음 주소로 이동해서 오프셋을 하기 때문에 배열보다 빠르다고 할 수 있다

- 하지만 사실 개미 눈꼽만큼의 차이일 것이다...!

---



# sizeof 연산자에서의 차이


```c
int nums[3] = { 1, 10, 100 };

int* ptr = nums;

size_t size1 = sizeof(nums); /* 12 = 3 * 4 */
size_t size2 = sizeof(ptr);  /* 4 */
```

- sizeof(배열)과 sizeof(포인터)는 다른 값을 반환
  - sizeof(배열) : 배열의 총 크기를 반환
  - sizeof(포인터) : 포인터의 크기를 반환
- 그 이유는?
  - 포인터는 진짜 주소만 저장하고 있기 때문이다.
  - 위를 예로 하자면 ptr은 nums[0]번째 주소를 가지고 있기 때문이다.

---


# 문자열 초기화


### 방법 1

```c
char day1[] = "42seoul";
```


- 배열에 차례대로 저장이 되고 마지막에 널문자(’\0’)가 들어가고, 한수 안에서 이렇게 배열을 선언하고 초기화하게 된다면 스택 메모리에 저장이 된다.


### 방법 2


```c
char* day2 = "42seoul";
```


- 포인터 변수는 스택에 저장이 되고 실제 문자열은 데이터 섹션에 저장이 된다.
- 그래서 문자열을 수정할 수가 없다. 수정할 경우 ‘결과가 정의되지 않음’오류가 나온다. 그래서 이렇게 할 경우 읽기전용이라고 할 수 있다.

---


# 대입


- 포인터 변수에 값을 대입할 수 있으나 배열 변수에는 할 수 없음


```c
int* ptr1;
int* ptr2;
int arr1[5];
int arr2[5];
int x = 5;

ptr1 = arr1;
arr1 = ptr1; /* 컴파일 오류 */

ptr1 = &x;
arr1 = &x; /* 컴파일 오류 */

ptr1 = ptr2;
arr1 = arr2; /* 컴파일 오류 */
```

- 포인터 변수에는 주소 값을 대입할 수 있고, 배열 변수에는 대입할 수 없다.

  배열은 한번 만들어지면 주소가 고정이 된다. 그래서 그 주소를 바꿀 수가 없다..!!


---


# 포인터 산술 연산


- 포인터는 산술 연산이 가능하지만 배열은 불가능
- 배열의 주소를 증가하거나 감소하고 싶다면 포인터에 배열의 주소를 대입 후 그 포인터 변수를 증가/감소하면 됨

```c
++ptr;
--ptr;

ptr += 1;
ptr -= 1;

++arr; /* 컴파일 오류 */
--arr; /* 컴파일 오류 */

arr += 1; /* 컴파일 오류 */
arr -= 1; /* 컴파일 오류 */
```

- 포인터는 산술 연산{후위연산자(++, - -), 전위연산자(++, - -) 등} 가능하다. 하지만 배열은 불가능하다!
- 배열의 주소를 증가하거나 감소하고 싶다면 포이니터 배열의 주소를 대입 후 그 포인터 변수를 증가/감소 하면 된다.
- 그리고 우리가 자주 사용하듯이 [ ] index를 계산을 해도 된다!
