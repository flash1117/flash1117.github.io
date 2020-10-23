---
layout: post
title: "Programmers - 문자열 압축"
date: 2020-05-03 13:00:59
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

string getCompression(string s, int num) {

    string ret = "";
    vector<string> vec;
    int index =0;

    while(index < s.length()) {
        string temp = "";
        for(int i = index; i<index+num; i++) {
            if(i<s.length())
                temp += s[i];
        }
        vec.push_back(temp);
        index += num;
    }

    index =1;
    for(int i=0; i<vec.size(); i++) {
        int cnt =1;
        for(int j = i+1; j<vec.size(); j++){
            if(vec[i] == vec[j]){
                cnt++;
            } else break;
        }

        if(cnt > 1) {
            i += cnt-1;
            ret+= to_string(cnt) + vec[i];
        } else {
            ret += vec[i];
        }
    }

    return ret;
}

int solution(string s) {
    int answer = s.length();
    string temp = "";
    for(int i=1; i<s.length()/2+1; i++) {

        temp = getCompression(s, i);
    //    cout << temp << endl;
        if(temp != "")
            answer = answer > temp.length() ? temp.length() : answer;

    }

    return answer;
}
```
