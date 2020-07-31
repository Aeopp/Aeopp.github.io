---
layout: post
title:  C++ future promise async 사용시 주의사항
gh-repo: Aeopp/Multithread_programming
gh-badge: [star, fork, follow]
tags: [주의사항?,C++,Multi thread enviroment]
comments: true
---
* ### async 의 return value (future object) 를 무시하면  launch policy 를 async 로 설정하였더라도 task는  동기적으로 수행된다. 
* ### async 로 launch 된 task 는 공유메모리에 대해 접근순서 동기화를 수행한다.

각종 테스트를 해보면서 값을 관찰하였는데 async 함수 호출시 반환되는 future 객체를 버리면 nodiscard attribute 경고가 나타난다.(에러는 아님) 
문제는 future 객체를 받지않고 리턴값을 버리면 async 로 호출한 함수가 동기적으로 호출된다는것....
 해당함수의 작업이 끝날때까지 blocking 될텐데 이러면 사용하는 의미가 없다.
 (일반함수 호출을 하고말지)
 
cppreference 로 명세를 읽어보아도 언급을 하지 않는...것 같다 (내 영어가 짧아서 놓친걸수도..)

또한 async 로 실행되는 task 는 내부적으로 lock 를 건다든지 해서 공유메모리에 대해 접근순서 동기화를 해주는것 같다.  atomic 나 semaphore 를 사용하지 않아도 
race condition 이 일어나지 않는다....

신통방통하다 정말.... 테스트를 아무리 해보아도 race condition 이 일어나지 않는다.  솔직히 지금 심정은 마법을 쓰는것 같으며 머리속이 매우 복잡하다 어떻게 구현하였는지 힌트라도 누가 알려줬음 좋겠다....  

아직 갈길이 멀구나 ~ 
