---
title: "JavaScript 조건문 문제 풀이"

categories:
  - Coding Test Lesson
tags:
  - [JavaScript, Coding Test, stdin, stdout]

toc: true
toc_sticky: true

---

# 혼자 힘으로 풀어보기

- **문제 제목**: 시험 성적
- **문제 난이도**: 별1
- **문제 유형**: 기초 문법
- **추천 풀이 시간**: 10분
- 시험 성적: https://www.acmicpc.net/problem/9498

```javascript
const fs = require('fs');
const input = fs.readFileSync('/dev/stdin').toString().split('\n');

const num = parseInt(input[0]);
const score = "ABCDF";
let outputIndex = 0;

if (num >= 90) {
  outputIndex = 0;
} else if (num >= 80) {
  outputIndex = 1;
} else if (num >= 70) {
  outputIndex = 2;
} else if (num >= 60) {
  outputIndex = 3;
} else {
  outputIndex = 4;
}
console.log(score[outputIndex]);
```

​    

# 혼자 힘으로 풀어보기

- **문제 제목**: 알람 시계
- **문제 난이도**: 별1
- **문제 유형**: 기초 문법
- **추천 풀이 시간**: 10분
- 시험 성적: https://www.acmicpc.net/problem/2884

```javascript
const fs = require('fs');
const input = fs.readFileSync('/dev/stdin').toString().split('\n');

const tmp = input[0].split(' ');
let time = parseInt(tmp[0]);
let min = parseInt(tmp[1]);

function parseTime(time, min) {
  return ((time + 23) + parseInt((min + 15) / 60)) % 24;
}

function parseMin(min) {
  return ((min + 15) % 60);
}

console.log(`${parseTime(time, min)} ${parseMin(min)}`);
```

