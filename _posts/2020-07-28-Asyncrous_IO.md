---
layout: post
title: 비동기 I/O 연산시 주의점
subtitle:  
gh-repo: Aeopp/os_system_programming
gh-badge: [star, fork, follow]
tags: [Operating System]
comments: true
---

## 비동기 I/O 연산을 통해서 파일에 쓰기작업을 동시접근해서 하는 경우 해당 파일핸들이 가리키는 커널 오브젝트의 파일 포인터는 의미가 없다.

1. (A,B,C) 함수가 호출되었다고 가정해보자 
2. 그리고 C 함수를 호출하기 전까지 콜백함수 알림을 받지않는다고 가정한다.

A,B,C, 함수에 의해서 파일에 데이터를 동시에 쓰고있는 상황이고 어떤 함수가 언제 끝날지도 알 수 없고 그 순서도 불분명하다
이러한 상황에서 커널이 파일포인터를 어떻게 컨트롤 한단 말인가??

파일포인터를 이용해서 문제를 해결할려고하면 매우 어려워진다 

이 경우 A B C 가 Write 하려는 데이터의 크기를 구한 다음 데이터의 크기만큼 Offset 을 적용하는 방식으로
문제를 해결해야 한다.

