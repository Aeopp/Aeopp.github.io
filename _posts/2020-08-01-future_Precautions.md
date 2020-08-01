---
layout: post
title: future promise async 사용시 주의사항
subtitle:
gh-repo: Aeopp/Multithread_programming
gh-badge: [star, fork, follow]
tags: [Multi-thread, System,C++]
---

* async 의 return value (future object) 를 무시하면  launch policy 를 async 로 설정하였더라도 task는  동기적으로 수행된다. 
* async 로 launch 된 task 는 공유메모리에 대해 접근순서 동기화를 수행한다.

         1 async(launch::async,f);
         2 async(launch::async,g);

호출시 반환값을 버리면 1번라인의 실행이 끝날때 까지 2번라인이 blocking 되는걸 볼 수 있다.
### 왜 blocking 되는 걸까? async 는 비동기화 호출인데 ?? 
async 함수 호출로 생성된 future 객체들중 마지막으로 소멸되는 객체의 소멸자가 task 가 끝날때 까지 blocking 되기 때문이다.


또한 async 로 실행되는 task 는 내부적으로 lock 를 건다든지 해서 공유메모리에 대해 접근순서 동기화를 해주는것 같다.  
atomic 나 semaphore 를 사용하지 않고 아무리 테스트를 해보아도 race condition 이 일어나지 않는다.
스콧 마이어스 아저씨한테 물어보고 싶네 책을 뒤져봐도 없고 답답하다.
