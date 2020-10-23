---
layout: post
title: "Programmers - 스킬트리"
date: 2020-05-02 13:00:59
author: mollangzzang
categories: Algorithm
tags: Algorithm 구현
cover: "/assets/algorithm.png"
---

```
#include <string>
#include <vector>
//#include <iostream>

using namespace std;

bool visited[30];
int rel[30];


void skillInit(string skill) {

    for(int i=0; i<30; i++)
        rel[i] = -2;

    rel[skill[0]-'A'] = -1;

    for(int i = 1; i<skill.length(); i++) {
        rel[skill[i]-'A']= skill[i-1]-'A';
    }

  //  for(int i=0; i<30; i++)
    //    cout << rel[i] << " ";
}

void visitedInit(string skill) {

    for(int i=0; i<skill.length(); i++) {
        visited[skill[i]-'A'] = false;
    }

}

int solution(string skill, vector<string> skill_trees) {
    int answer = skill_trees.size();
    skillInit(skill);

    for(int i=0; i<skill_trees.size(); i++) {
        for(int j=0; j<skill_trees[i].length(); j++) {

            int curIndex = skill_trees[i][j]- 'A';
            if(rel[curIndex] == -2) continue;
            else if(rel[curIndex] == -1) {
                visited[curIndex] = true;
            }
            else {
                int prev = rel[curIndex];
      //          cout << "cur : " << curIndex << " prev : " << prev;
                if(visited[prev]) {
                    visited[curIndex] = true;
                } else {
                    answer--;
                    break;
                }
            }

        }
        visitedInit(skill);
    }

    return answer;
}

```
