---
title: "문제 풀이를 위한 JavaScript 핵심 문법 알아보기"

categories:
  - Coding Test Lesson
tags:
  - [JavaScript, Coding Test]

toc: true
toc_sticky: true
---

## JavaScript 핵심 문법



### 알고리즘 코딩 테스트 문제의 입출력 형식  

- 알고리즘 문제에서는 적절한(약속된) 입출력양식이 주어진다
  1. 첫 번째 단계는 데이터를 **입력 받거나 생성**하는 것이다
  2. 이후에 적절한 알고리즘을 사용하여 **도출된 정답을 정확한 형식으로 출력**한다
- 예시) N명의 학생의 성적 데이터가 주어졌을 때, 이를 내림차순으로 정렬한 결과를 출력하라
- **입력 형식**
  - 첫째 줄에는 학생의 수 N이 자연수로 주어지고, 둘째 줄에 공백을 기준으로 하여 N명의 학생에 대한 성적이 정수 형태로 주어진다(2 <= N <= 1,000,  0 <= 성적 <= 100)
- **출력 형식**
  - N명의 학생의 성적을 내림차순 정렬한 결과를 첫째 줄에 공백을 기준으로 구분하여 출력하라
- **입력 예시**

``` bash
5
17 88 53 100 73
```



- **출력 예시**

```bash
100 88 73 53 17
```

  

### 코딩 테스트용 JavaScript 기본 출력

- 일반적인 알고리즘 문제를 풀 때, 표준 출력으로 console.log()를 이용한다

```javascript
// 단순히 문자열을 출력한다
console.log('Hello World!');

result = 35;
// 템플릿 리터럴을 사용해 문자열 내부에 변수를 포함한다 (백틱 문자 사용)
console.log(`정답은 ${result}입니다.`);
```

  

### 코딩 테스트용 JavaScript 기본 사칙 연산

- JavaScript 프로그래밍 언어에서는 기본적인 사칙 연산 기능을 제공한다

``` javascript
a = 7;
b = 3;

console.log(a + b);
console.log(a - b);
console.log(a * b);
console.log(parseInt(a / b)); // 몫만 남기기
console.log(a % b);
```

  

### 코딩 테스트용 JavaScript 빠른 출력

- JavaScript로 코딩 테스트 문제를 풀 때, 출력 과정만으로 시간 초과를 받을 때가 있다
- **출력 시간을 단축**하기 위해 다음과 같은 방법을 유용하게 사용할 수 있다

```javascript
let answer = '';

/*
여러 출력 결과를 한 줄에 하나씩 출력할 때 매번 console.log()를 실행하지 않고, 하나의 문자열에 결과를 저장해서 한꺼번에 출력하는 것이 대개 더 빠르게 수행한다
*/
for (let i = 0; i <= 100; ++i) {
  answer += i + '\n'; // 문자열로 변환하여 기록
}

console.log(answer);
```

  

### 코딩 테스트용 JavaScript 기본 입력 - fs 모듈

- 입력 데이터가 텍스트 파일 형태로 주어지는 경우, **파일 시스템 모듈**을 사용한다
- 예를 들어 /dev/stdin 파일에 적힌 텍스트를 읽어오는 경우, 다음과 같이 코드를 작성한다
- **기능**
  - 전체 텍스트를 읽어 온 뒤에, 줄바꿈 기호를 기준으로 구분하여 리스트로 변환하기

```javascript
// readline 모듈보다는 fs를 이용해 파일 전체를 읽어 들여 처리하기
let fs = require('fs');
let input = fs.readFileSync('/dev/stdin').toString().split('\n');
// let input = fs.readFileSync('input.txt').toString().split('\n');

console.log(input);
```



