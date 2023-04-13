---
title: "JavaScript 입출력 문제 풀이"

categories:
  - Coding Test Lesson
tags:
  - [JavaScript, Coding Test, stdin, stdout]

toc: true
toc_sticky: true
---

### 혼자 힘으로 풀어보기

- **문제 제목**: Hello World
- **문제 난이도**: 별1
- **문제 유형**: 기초 문법
- **추천 풀이 시간**: 5분
- Hello World: http
s://www.acmicpc.net/problem/2557

```javascript
console.log("Hello World!");
```



### 문제 풀이 핵심 아이디어

- JavaScript를 이용해 문자열을 출력 할 수 있어야 한다
- console.log() 함수를 이용해 원하는 변수 혹은 상수를 출력할 수 있다



### 혼자 힘으로 풀어보기

- **문제 제목**: A+B
- **문제 난이도**: 별 1개
- **문제 유형**: 기초 문법
- **추천 풀이 시간**: 5분
- A+B: https://www.acmicpc.net/problem/1000

```javascript
const fs = require('fs');
const input = fs.readFileSync('/dev/stdin').toString().split('\n');

const line = input[0].split(' ');

const a = parseInt(line[0]);
const b = parseInt(line[1]);
console.log(a + b);
```





### 문제 풀이 핵심 아이디어

- JavaScript를 이용해 정수를 처리해야 한다
- 이를 위해, 입력 받은 문자열 데이터를 정수로 변환해야 한다
- 이후에 덧셈을 수행한 결과를 출력한다
- fs 모듈을 이용해 특정 파일에 문자열을 읽어 올 수 있다



### 혼자 힘으로 풀어보기

- **문제 제목**: A*B
- **문제 난이도**: 별 1개
- **문제 유형**: 기초 문법
- **추천 풀이 시간**: 5분
- A*B: https://www.acmicpc.net/problem/10998

```javascript
const fs = require('fs');
const input = fs.readFileSync('/dev/stdin').toString().split('\n');

const line = input[0].split(' ');

const a = parseInt(line[0]);
const b = parseInt(line[1]);
console.log(a * b);
```



### 혼자 힘으로 풀어보기

- **문제 제목**: 사칙연산
- **문제 난이도**: 별 1개
- **문제 유형**: 기초 문법
- **추천 풀이 시간**: 5분
- 사칙연산 : https://www.acmicpc.net/problem/10869

```javascript
const fs = require('fs');
const input = fs.readFileSync('/dev/stdin').toString().split('\n');

const line = input[0].split(' ');

const a = parseInt(line[0]);
const b = parseInt(line[1]);
console.log(`${a + b}\n${a - b}\n${a * b}\n${parseInt(a / b)}\n${a % b}`);
```



### 혼자 힘으로 풀어보기

- **문제 제목**: 곱셈
- **문제 난이도**: 별 1개
- **문제 유형**: 기초 문법
- **추천 풀이 시간**: 15분
- 곱셈 : https://www.acmicpc.net/problem/2588

```javascript
const fs = require('fs');
const input = fs.readFileSync('/dev/stdin').toString().split('\n');

const a = parseInt(input[0]);
const b = input[1];

console.log(`
	${a * parseInt(input[1][2])}\n
	${a * parseInt(input[1][1])}\n
	${a * parseInt(input[1][0])}\n
	${a * parseInt(input[1])}
	`);
```

