---
layout: post
title: "2020-07-29 TIL"
date: 2020-07-29 13:00:59
author: mollangzzang
categories: TIL
tags: TIL
cover: "/assets/TIL.png"
---

### Linux

- Linux는 오픈소스이며 대부분 무료 OS이다.
- Linux는 무료이기에 잡지나 책을 통해 배포가 가능하다.
- 주 사용자는 개발자.
- Linux 의 커널은 커뮤니티에 의해 개발되었다.
- 다양한 컴퓨터 하드웨어에 설치가 가능하다 (모바일, 데스크탑, 슈퍼컴퓨터 ...)
- BASH는 Linux의 기본 Shell 이다. BASH는 다양한 명령어를 지원한다.
- 위협탐지와 해결이 매우 빠르다. 커뮤니티 기반이기에 Linux의 사용자가 위협에 대한 issue를 올리면 세계의 개발자들이 해결을 위한 작업을 시작한다.
- 1991년 9월 17일에 출시되었다.
- 종류로는 Ubuntu, Fedora, Red Hat, Debian, Archlinux, Android 등이 있다.
- Linux는 커널을 핵심으로 하고 Shell이 유저와 커널간의 인터페이스가 된다.

### Unix

- 대학, 회사 등의 큰 기업에서 선호하며 대부분 유료 OS이다.
- 유닉스 환경과 Client-Server 모델은 인터넷 개발의 필수 요소이다.
- Solaris 와 같은 무료 OS도 존재한다.
- 인터넷서버, 워크스테이션과 PC들에 사용된다. 금융인프라와 24x365 고 가용솔루션의 뼈대를 이루는 인프라에 사용된다.
- 초기에 유닉스는 커맨드기반의 OS였으나, GUI가 생성되어 공통 데스크톱 환경으로 불린다.

### bash 의 종류

- bash

Bourne Again Shell. 리눅스에서 가장 많이 사용하는 Shell이다. Bourne Shell과 호환되며 GNU project에 의해 만들어지고 배포되고 있다. 명령행 편집, 히스토리 치환 기능을 제공한다.

- csh

C Shell. 버클리에서 개발되었다. 명령행 편집기능은 제공하고 있지 않다.

- ksh

Korn Shell. 일반적으로 Unix에서 가장 많이 사용하고 있는 Shell 이며 Bourne Shell과 호환이된다.

- sh

Bourne Shell. 최초로 개발된 Shell이다.

- tcsh

확장 C Shell. 명령행 편집 기능을 제공한다.

- zsh

Z Shell. 가장 최근에 나온 Shell 이며 Bourne Shell 과 호환이 된다. 명령행 편집 기능을 제공한다.

### Windows 에서 Linux와 비슷한 환경을 가지고 싶다면?

> Windows 의 경우 git bash 또는 WSL(Window Subsysten for Linux) 를 사용하는 것이 가장 Linux와 비슷한 터미널 환경을 가지는 것 같다.

### Shell 이란?

> OS와 대화하는 프로그램

### 명령어의 종류

- pwd
  현재 디렉토리를 확인. 아래와 같이 출력된다.

- ls
  현재 디렉토리의 내용을 보여줌.

- mkdir
  새로운 디렉토리 생성

- cat filename
  파일 내용 표시

- less filename
  긴 파일의 내용을 끊어서 표시 q : 종료 g : 처음으로 G : 끝으로 /단어 : 문서에서 '단어'를 검색 space, enter, 화살표, hjkl : 페이지 이동

- history
  명령어 이력표시

- cp, mv, rm
  파일복사, 이동, 삭제

- find 디렉토리 -name "filename"
  지정한 디렉토리와 그 하위디렉토리에서 해당 파일을 검색한다.

- touch "파일이름"
  0btye 파일 생성

### SSH

SSH의 동작과정은 웹 브라우저의 request, response와 흡사한 형태를 가지고 있다.
우리는 Server 컴퓨터를 관리해야하는데, 그 때 명령어를 사용한다. 하지만 우리가 있는 환경은 Client 컴퓨터이며 따라서 명령어를 통하여 SSH Server를 제어하며 SSH Server는 해당 명령을 수행함으로써 서버컴퓨터를 제어하고 Client에게 알맞은 결과값을 응답해주게 된다.
