---
layout: post
title:  "Dynamic Programming"
date:   2019-10-15 13:00:59
author: mollangzzang
categories: Algorithm
tags:	Algorithm DynamicProgramming 동적계획법
cover:  "/assets/algorithm.png"
---

### Dynamic Programming

```
int fibo(int n) {

if(n == 1 || n == 2) return 1;
else return fibo(n-2) + fib(n-1);

}
```

대부분 DFS를 처음 배울 때 무조건 구현해보게 된다는 피보나치 수열을 Recursion 으로 구현한 코드이다. 물론 가장 단순하게 구현하는 방법이긴 하지만, 구하고자 하는 값이 크면 클수록 같은 계산을 많이 반복하게 되기 때문에 매우 비효율적이다. 

그래서 좀더 효율적인 방법이 없을까? 라고 고안된 방법이 **동적 계획법**이며, 이를 위해 알아 두어야 할 개념으론 **메모이제이션(memoization)**이 있다.

**메모이제이션**이란?
- 컴퓨터 프로그램이 동일한 계산을 반복해야 할 때, 이전에 계산한 값을 메모리에 저장함으로써 동일한 계산의 반복 수행을 제거하는 것이다.

위에 코드로 예를 들자면, 계산의 중복을 피하기 위해 이미 `fibo(5)` 값을 계산을 했다면, 배열에 저장을 해두어서 중복을 피하는 방법인 것이다.

이 때 배열을 **캐시(cache)** 라고 하고, 읽어 오는 과정은 **캐싱(caching)**이라고 한다.

```
init(f);

int fibo(int n) {

    if(n==1 ||n==2) return 1;
    else if(f[n] != -1) return f[n]; // -1은 초기화 시킨 값
    else {
        f[n] = f[n-2] + f[n-1];
        return f[n];
    }
}
```

메모이제이션을 적용시킨 코드는 위와 같이 될 것이다.

이 방식을 제외하고 한가지 더 중복을 피하는 방법이 있는데, **bottom-up** 방식이다.

이름에서 알 수 있듯이, 작은 것 부터 올라오는 방법이다.
이 방법의 핵심은 `f[n]` 의 값을 알기 위해서 `f[1]` 부터 순차적으로 값을 계산하며 `f[n]` 까지 도달해 왔다는 것이며 값을 구하긴 위해선 단순히 `f[n-1] + f[n-2]` 를 해주면 된다.

말만 들어선 무슨 소리냐 할 수 있을법 한데, 코드는 아래와 같다.

```
int fibo(int n) {

    f[1] = f[2] =1;
    for(int i=3; i<=n; i++)
        f[n] = f[n-1] + f[n-2];
    return f[n];
}
```

한가지 예를 더 들어보면 **이항계수 (Binomial Coefficient)**를 구하는 방법인데,
수학적 공식을 사용하면 `nCk =  n!/(n-k)! x k!` 이다.

문제는 이 식을 이용해서 단순 계산을 할 경우에는 컴퓨터에서 허용하는 정수 값을 초과할 위험이 있다는 것이다.

따라서 공식을 사용하지 않고 DFS를 이용하여 구현하면

```
int binomial(int n, int k) {

    if(n == k || k == 0) return 1; // base case
    else // general case
        return binomial(n-1,k) + binomial(n-1, k-1);
}
```
다음과 같다.


```
int binomial(int n, int k) {

    if(n == k || k == 0) return 1; // base case
    else if(bino[n][k] != -1) return bino[n][k];
    else // general case {
        bino[n][k] =binomial(n-1,k) + binomial(n-1, k-1);
        return bino[n][k]; 
    }
}
```
**memoization**방식 이며, 변수가 2개 이므로 이차원 배열을 생성하여 값을 설정해 주었다.


```
int binomial(int n, int k) {

    for(int i =0; i<=n; i++) {
        for(int j=0; j<=k&& j<=i; j++){
            if(k==0 || n==k) bino[i][j] = 1;
            else
                bino[i][j] = bino[i-1][j-1] + bino[i-1][j];
        }
    }
    return bino[n][k];
}

```

**bottom-up**방식이며, 다만 주의해야 할 점은 우리가 원하는 값보다 항상 오른쪽 항의 값이 구해져 있어야 한다는 것이다.