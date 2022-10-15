---
layout: post
title:  "[파이썬 코딩테스트 팁] Swap"
date:   2020-06-16
tags: [python, coding-test]
---
파이썬에는 C++처럼 두 변수의 값을 바꾸는 함수가 따로 없다. 다만 다음과 같이 튜플을 이용해 두 변수의 값을 바꿀 수 있다.
```python
a = 1; b = 2
(a, b) = (b, a)
# a = 2, b = 1
```
세 개 이상의 변수도 다음과 같이 swap할 수 있다.
```python
a = 1; b = 2; c = 3
(a, b, c) = (b, c, a)
# a = 2, b = 3, c = 1
```
리스트 안에 있는 원소들끼리도 자리를 바꿀 수 있다.
```python
new_list = [3, 8]
(new_list[0], new_list[1]) = (new_list[1], new_list[0])
# new_list = [8, 3]
```
이를 다음과 같이 함수로도 만들 수 있다.
```python
def swap(lst: list, i: int, j: int) -> None:
    """
    리스트 lst의 i번째 원소와 j번째 원소를 swap한다.
    """
    (lst[i], lst[j]) = (lst[j], lst[i])
```
이렇게 만든 함수는 퀵소트 등을 구현할 때 유용하게 쓸 수 있다.