---
layout: post
title:  "Dynamic Programming (2)"
date:   2019-10-17 13:00:59
author: mollangzzang
categories: Algorithm
tags:	Algorithm DynamicProgramming 동적계획법
cover:  "/assets/algorithm.png"
---

### Dynamic Programming

* 정수들이 저장된 n x n 행렬의 좌상단에서 우하단까지 이동한다. 단 오른쪽이나 아래 방향으로만 이동이 가능할 때, 방문한 칸에 있는 정수들의 합이 최소화 되도록 하라.

| | | | |
|:---:|:---:|:---:|:---:|
|6|7|12|5|
|5|3|11|18|
|7|17|3|3|
|8|10|14|9|

사실 다익스트라 알고리즘을 사용해서 최단경로 처럼 풀수도 있는 문제이지만, 굳이 동적계획법으로 풀어 본다면,

* (i,j) 까지 온다고 가정했을때 만드시 (i,j-1) 또는 (i-1,j) 행을 거쳐서 와야 하며 (i,j-1) 또는 (i-1,j) 까지 도달 할 때에도 최소의 비용으로 도착해야 한다는 것이다.

* 하지만 이 둘 중에 뭐가 최선인지는 모르기 때문에 둘의 크기를 비교하여 작은 것을 고른다.

* 다만 i == 1 또는 j == 1 일 때는 선택할 두개의 노드가 있는 것이 아니기 때문에 한가지 경우의 수는 따로 지정을 해주어야 한다.

```
#include <iostream>
#include <algorithm>

using namespace std;

int mat(int i, int j){

    if(i == 1 && j == 1) return m[i][j];
    else if (i == 1) return mat(1,j-1) + m[i][j];
    else if (j == 1) return mat(i-1,1) + m[i][j];
    else
        return min(mat(i-1, j), mat(i,j-1)) + m[i][j];
}
```

이 코드에 Memoization 을 적용하여 중복 계산을 피해준다면

```
int m[N][N];
int dp[N][N];

int mat(int i, int j){

    if(dp[i][j] != '초기화해준 값') return dp[i][j];
    if(i == 1 && j == 1) dp[i][j] = m[i][j];
    else if (i == 1) dp[i][j] = mat(1,j-1) + m[i][j];
    else if (j == 1) dp[i][j] = mat(i-1,1) + m[i][j];
    else
        dp[i][j] = min(mat(i-1, j), mat(i,j-1)) + m[i][j];
    return dp[i][j];
}
```

만약 Bottom-up 방식으로 구현을 하게 된다면,

```
int mat() {

    for(int i=1; i<=n; i++) {

        for(int j=1; j<=n; j++){
            if(i == 1 && j ==1)
                dp[i][j] = m[i][j];
            else if(i==1)
                dp[i][j] = m[i][j] + dp[i][j-1];
            else if(j==1)
                dp[i][j] = m[i][j] + dp[i-1][j];
            else
                dp[i][j] = m[i][j] + min(dp[i-1][j],dp[i][j-1]);

        }
    }
    return dp[n][n];
}

```