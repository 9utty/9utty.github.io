---
title: "[Programming] C++ 상속"
date: 2022-02-09 18:32:30 +0800
categories: [Programming Language, C++]
tags: [c++]  
---

# 상속

- 상속 문법 사용하기

  - 공통의 특징을 모은 클래스를 설계한다.

  ```cpp
  class Person
  {
  	std::string name;
  	int age;
  };
  
  class Professor : public Person
  {
  	int major;
  };
  
  class Student : public Person
  {
  	int id;
  };
  
  int main ()
  {
  	Professor p;
  	Student s;
  }
  ```

  - 한 클래스가 다른 클래스에서 정의된 속성들(데이터, 함수)를 이어 받아서 사용하는 것
  - 이미 정의도니 클래스를 기반으로 새로운 클래스 설계
  - S/W의 재사용성 지원

- 상속 문법의 장점

  - 코드의 중복을 막을 수 있다.
  - 상속을 통해서 기존 클래스에 새로운 특징을 추가한 새로운 타입의 설계

- protected

  - 외부에서는 접근할 수 없지만, 파생클래스에서는 접근할 수 있는 멤버