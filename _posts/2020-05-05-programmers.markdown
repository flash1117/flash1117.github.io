---
layout: post
title: "Programmers - 괄호 변환"
date: 2020-05-05 13:00:59
author: mollangzzang
categories: Algorithm
tags: Algorithm 구현 DFS
cover: "/assets/algorithm.png"
---

```
#include <string>
#include <vector>

using namespace std;

string getCorrect(string u) {

    int left =0;
    int right =0;
    bool isCorrect = true;
    string _u = "";
    string _v = "";

    if(u == "") return "";

    for(int i=0; i<u.length(); i++) {
        if(u[i] == '(') left++;
        else right++;

        if(right > left) isCorrect =false;

        _u += u[i];

        if(left >0 && right > 0 && left == right) {
            for(int j=i+1; j<u.length(); j++)
                _v += u[j];
            break;
        }
    }

    if(isCorrect) {
        // u가 올바른 문자열
        return _u + getCorrect(_v);
    }
    else {
        string ret = "(" + getCorrect(_v) + ")" ;
        for(int i=1; i<_u.length()-1; i++) {
            if(_u[i] == '(') ret += ")";
            else ret += "(";
        }
        return ret;
     }

}


string solution(string p) {
    string answer = "";

    answer = getCorrect(p);

    return answer;
}

```
