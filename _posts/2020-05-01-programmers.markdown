---
layout: post
title: "Programmers - 카카오프렌즈 컬러링북"
date: 2020-05-01 13:00:59
author: mollangzzang
categories: Algorithm
tags: Algorithm BruteForce
cover: "/assets/algorithm.png"
---

```
#include <queue>
#include <vector>

using namespace std;

// 전역 변수를 정의할 경우 함수 내에 초기화 코드를 꼭 작성해주세요.

int dx[] = {0,0,-1,1};
int dy[] = {-1,1,0,0};
bool visited[101][101];
typedef struct {
    int x, y, cnt;
}Pos;

bool isBoundary(int x, int y, int m, int n) {

    if(x<0 || y<0 || x>m-1 || y>n-1) return false;
    return true;

}

int getArea(int x, int y, int m, int n, vector<vector<int>> picture) {

    queue<Pos> q;
    q.push({x,y,1});
    visited[x][y] = true;

    int ret =0;
    while(!q.empty()) {

        int curX= q.front().x;
        int curY = q.front().y;
        int ccnt = q.front().cnt;
        ret++;
        q.pop();

        for(int i=0; i<4; i++)
        {
            int nextX= curX + dx[i];
            int nextY = curY + dy[i];

            if(isBoundary(nextX, nextY, m,n) && !visited[nextX][nextY] && picture[nextX][nextY] == picture[x][y])
            {
                visited[nextX][nextY] = true;
                q.push({nextX, nextY, ccnt+1});
            }
        }

    }

    return ret;
}


vector<int> solution(int m, int n, vector<vector<int>> picture) {
    int number_of_area = 0;
    int max_size_of_one_area = 0;

    vector<int> answer(2);

    const int row = m;
    const int col = n;

    for(int i=0; i<row; i++)
        for(int j=0; j<col; j++)
            visited[i][j] = false;
    int ret =0;
    for(int i=0; i<row; i++)
    {
        for(int j=0; j<col; j++) {
            if(!visited[i][j]) {
                ret = getArea(i,j,m,n,picture);
                if(picture[i][j] != 0) {
                    number_of_area++;
                    max_size_of_one_area = max_size_of_one_area > ret ? max_size_of_one_area : ret;
                }

            }
        }
    }

    answer[0] = number_of_area;
    answer[1] = max_size_of_one_area;
    return answer;
}

```
