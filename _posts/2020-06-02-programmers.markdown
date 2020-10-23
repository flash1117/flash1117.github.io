---
layout: post
title: "Programmers - 다리를 지나는 트럭"
date: 2020-06-02 13:00:59
author: mollangzzang
categories: Algorithm
tags: Algorithm 구현
cover: "/assets/algorithm.png"
---

```
#include <string>
#include <vector>
#include <queue>
using namespace std;

int solution(int bridge_length, int weight, vector<int> truck_weights) {
    int answer = 0;
    int index = 0;
    int extra_weight = weight;

    queue<pair<int,int>> q;

    while(1) {
        if(index == truck_weights.size() && q.empty()) break;
        answer++;



        int q_size = q.size();

        if(index < truck_weights.size() && truck_weights[index] <= extra_weight) {
            q.push({truck_weights[index], 1});
            extra_weight -= truck_weights[index];
            index++;
        }


        for(int i=0; i<q_size; i++) {
            int _weight = q.front().first;
            int _time = q.front().second;
            q.pop();

            if(_time == bridge_length){
                extra_weight += _weight;
            }
            else q.push({_weight, _time+1});
        }

    }

    return answer;
}

```
