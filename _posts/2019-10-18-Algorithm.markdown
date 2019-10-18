---
layout: post
title:  "Dynamic Programming (3)"
date:   2019-10-17 13:00:59
author: mollangzzang
categories: Algorithm
tags:	Algorithm DynamicProgramming 동적계획법
cover:  "/assets/algorithm.png"
---

### Dynamic Programming

1. 일반적으로 최솟값, 최댓값 또는 카운팅 문제에 적용 된다.

2. 주어진 문제에 대한 점화식을 정의한다.

3. 푸는 방법은 Memoization 또는 Bottom-Up 방식으로 풀게 된다.

다만 동적 계획법이 어려운 이유는 적절한 점화식을 세우는 부분이 어렵기 때문이다.

그래서 a 가 c 까지 최단경로로 간다고 가정 했을 때, 중간에 거쳐가야 하는 지점 b 까지 무조건 최단 경로로 왔는가 라는걸 생각해보아야 하는 것이다.

#### Matrix-Chain Multiplication

이 문제는 Dynamic Programming 에서 유명한 예 중 하나이다. 두 행렬을 곱할 때의 특징을 이용한 문제이다.

```
#include <iostream>

using namespace std;

void product(int A[][], int B[][], int C[][]){
    for(int i=0; i<p; i++) {
        for(int j=0; j<r; j++){
            C[i][j] =0;
            for(int k =0; k<q; k++)
                C[i][j] += A[i][k]*B[k][j];
        }
    }

}

```
위 코드는 두 개의 행렬을 곱할 때 코드를 간단하게 짠 것이다. 여기서 곱셈연산의 횟수는 p x q x r 개가 된다.

행렬은 교환 법칙은 성립하지 않지만 결합 법칙은 성립하며,이 특성을 이용한 문제인데, 어떤 것을 먼저 계산하느냐에 따라서 곱셈 연산횟수가 달라지게 되는데 어떤 것이 최선의 방법이냐 를 묻는 것이다.

예를 들어 A1 A2 A3 가 있고 A1 행렬은 3x100 A2 행렬은 100 x 5 A3 행렬은 5 x 200 이라고 가정한다면

A1과 A2 행렬을 먼저 곱한다면 A3와 곱할 행렬은 3x5가 된다.

하지만 A2 와 A3 을 먼저 곱하면 A1 과 곱할 행렬은 100 x 200 의 크기를 가져서 곱셈 횟수가 더욱 늘어나게 될 것이다.

```
int matrixChain(int n){

    for(int i =1; i<=n; i++) m[i][j] =0; // 가운데 채우고 시작
    for(int r =1; r<=n-1; r++) {
        for(int i = 1; i<=n-r; i++) {
            int j = i+r;
            m[i][j] = m[i+1][j] + p[i-1]*p[i]*p[j];
            for(int k = i+1; k<=j-1; k++) {
                if(m[i][j] > m[i][k] + m[k+1][j] + p[i-1]*p[k]*p[j]);
                    m[i][j] = m[i][k] + m[k+1][j] + p[i-1]*p[k]*p[j]
            }
        }
        return m[1][n];
    }


}

```