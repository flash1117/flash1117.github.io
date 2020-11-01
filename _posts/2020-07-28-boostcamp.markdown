---
layout: post
title: "2020-07-28 TIL"
date: 2020-07-28 13:00:59
author: mollangzzang
categories: TIL
tags: TIL
cover: "/assets/TIL.png"
---

```
"use strict";

let keyboard = [
  ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0"],
  ["Q", "W", "E", "R", "T", "Y", "U", "I", "O", "P"],
  ["A", "S", "D", "F", "G", "H", "J", "K", "L", ";"],
  ["Z", "X", "C", "V", "B", "N", "M", ",", ".", "?"],
];

let dx = [-1, 1, 0, 0];
let dy = [0, 0, -1, 1];

const example = ["BOOST", "HELLO,CAMPER5;", "FROM.1984"];
const col = keyboard[0].length;
const row = keyboard.length;

/*
function getStartPoint(keyboard) {
  for (let i = 0; i < keyboard.length; i++) {
    for (let j = 0; j < keyboard[i].length; j++) {
      if (keyboard[i][j] === "1") return [i, j];
    }
  }
}
*/

function isBoundary(x, y) {
  if (x < 0 || y < 0 || x > row - 1 || y > col - 1) return false;
  return true;
}

function create2DArray(row, col) {
  let ary = new Array(row);
  for (let i = 0; i < row; i++) {
    ary[i] = new Array(col);
    for (let j = 0; j < col; j++) {
      ary[i][j] = 0;
    }
  }
  return ary;
}

function initArray(ary) {
  for (let i = 0; i < ary.length; i++) {
    for (let j = 0; j < ary[i].length; j++) {
      ary[i][j] = 0;
    }
  }
  return ary;
}

function getCharByMoveDir(index) {
  if (index == 0) return "^";
  else if (index == 1) return "_";
  else if (index == 2) return "<";
  else return ">";
}

let visited = create2DArray(row, col);

function getPath(srcX, srcY, dstValue, visited) {
  let q = [];
  q.push([srcX, srcY, ""]);
  visited[srcX][srcY] = 1;
  while (q.length) {
    let cur = q.shift();
    let curX = cur[0];
    let curY = cur[1];
    let path = cur[2];

    if (keyboard[curX][curY] == dstValue) {
      return [curX, curY, path + "@"];
    }

    for (let i = 0; i < 4; i++) {
      let nextX = curX + dx[i];
      let nextY = curY + dy[i];

      if (isBoundary(nextX, nextY) && visited[nextX][nextY] === 0) {
        q.push([nextX, nextY, path + getCharByMoveDir(i)]);
        visited[nextX][nextY] = 1;
      }
    }
  }

  return -1;
}

// const startPoint = getStartPoint(keyboard);

let startPoint = {
  x: 0,
  y: 0,
};

for (let i = 0; i < example.length; i++) {
  let ret = "";
  startPoint.x = 0;
  startPoint.y = 0;
  process.stdout.write("문자열 : " + example[i]);
  console.log();
  for (let j = 0; j < example[i].length; j++) {
    visited = initArray(visited);

    let ans = getPath(startPoint.x, startPoint.y, example[i][j], visited);
    if (ans != -1) {
      startPoint.x = ans[0];
      startPoint.y = ans[1];
      ret += ans[2];
    }
  }

  process.stdout.write(ret);
  console.log();
}

```

### 추가적으로 필요한 기능들

- async , await 을 이용한 동기적 방식의 구성
- 문자열 입력 받기
- 키보드의 자판 위치 바뀔 가능성이 있으므로 초기 시작지점 받을 함수 구현
- 입력받는 문자열이 커질수록 시간복잡도가 기하급수적으로 상승하므로 시간을 줄일 수 있는 테이블 구성.
- 키보드에 존재하지 않는 문자의 경우 예외 처리
- 함수단 조금 더 세분화 하여 구현

### 배운 점

- 문자열 입력을 받으려고 하다보니 비동기 처리를 해야 한다는 것을 알게 되었다. 그동안 C/C++ 위주로 코드를 작성하다보니 javascript 언어 자체의 특성을 잘 이해하지 못한채로 억지로 내가 알고 있는 틀에 끼워 맞추려 했던 것 같다.

- callback 은 호출하는 함수가 호출되는 함수로 전달하는 함수를 말하며 이때 callback 함수의 제어권은 호출되는 함수에게 있다. callback 함수는 setTimeout 함수와 같은 비동기 코드를 동기식으로 처리하기 위해 사용된다.

- 하지만 callback 만 남발하게 되면 callback 지옥에 빠질 수가 있다. 이러한 문제점을 해결하기 위해 나온 것이 promise 이다. 매개변수로 resolve 와 reject를 넘겨주며 promise 라는 객체를 반환하게 된다. 또한 반환 받은 객체를 then() 함수 이용하여 사용하게 된다. 실패한 경우는 catch()로 예외처리가 가능하다.

- 하지만 promise 를 보다 보기 쉽도록 만든 것이 await 과 async이다. async는 await 을 선언한 함수 내부에서만 동작하며 보다 동기적으로 프로그래밍 할 수 있도록 만들어 주는 것 같다.

- 위와 같은 개념을 공부하고 다시 위의 문제의 적용하려고 하니 하루아침에 될 것 같지는 않아서 조금 더 공부를 해봐야 할 것 같다. 당장 할 수 있는 일은 함수를 어떻게 쪼갤 것인지 좀더 생각하고 다른 사람이 보기에 적합한 함수명, commit 메세지를 좀 더 고민하는 것인 것 같다.

- `--single-branch` 옵션은 해당 프로젝트에 브랜치가 너무 많은 경우 브랜치 전부를 clone 하지 않고 특정 하나의 branch 만 clone 하기 위해 존재하는 것 같다.

- 그동안 커밋메세지를 작성함에 있어서 git commit -m "commit message" 와 같은 방식으로 작성을 하였다. 하지만 commit message 를 본문을 추가 시켜서 추가 할 수 도 있고 어설프게 영어로 작성한다면 후에 자신이 로그 기록을 볼 때도 좋지 않은 상황이 발생 할 수 있기에 커밋메세지를 명확하게 작성하는 것이 좋다는 것을 알게되었다.

- main 함수를 따로 생성하여 출력하는 방법이 나에게 있어서 더 맞는 것 같다.
