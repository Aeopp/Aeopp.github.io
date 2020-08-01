---
layout: post
title: future promise async 사용시 주의사항
subtitle:
gh-repo: Aeopp/Multithread_programming
gh-badge: [star, fork, follow]
tags: [Multi-thread, System,C++]
---

* async 의 반환값을 (std::future<T>) 무시하면  launch policy 를 async 로 설정하였더라도 task는  동기적으로 수행된다. 
* async 로 launch 된 task 는 공유메모리에 대해 접근순서 동기화를 수행한다.

         1 async(launch::async,f);
         2 async(launch::async,g);

호출시 반환값을 버리면 1번라인의 실행이 끝날때 까지 2번라인이 blocking 되는걸 볼 수 있다.
### 왜 blocking 되는 걸까? async 는 비동기화 호출인데 ?? 

async 함수 호출로 생성된 future 객체들중 마지막으로 소멸되는 객체의 소멸자가 task 가 끝날때 까지 blocking 되기 때문이다.
다르게 표현하자면 비동기적으로 실행되고 있는 스레드에 대해 암묵적으로 Join 을 수행하는 것이다.
마지막으로 파괴되지 않는 future 객체의 소멸자는 단지 해당 future 객체를 파괴할 뿐이다. 정상적인 소멸자의 행동이다.
이것은 암묵적인 detach를 수행한다고 생각하면 된다. 때문에 deferred 옵션으로 async 를 launch 시켰을 경우의 마지막 future 객체가 소멸되었다면
그리고 그 이전에 wait 나 get 를 호출하지 않았다면 해당 Task 가 수행되지 않음을 뜻한다.

future 객체는 언제든지 shared_future 객체로 변환 될 수가 있으며 promise 의 반환값을 세팅하는것과 이러한 것이 맞물려 promise 와 future 객체 사이에는
공유상태라는 힙에 할당된 객체가 존재한다는 것을 알아야 한다. 이 객체는 마치 shared_ptr 의 컨트롤 블록처럼 
future 의 참조 카운팅을 관리한다 promise 객체는 Task 의 수행이 종료되면 이 객체에 반환값을 설정해준다. 

future 마지막 객체가 소멸되었을때 소멸자에서 blocking 되는 경우는 다음 조건들을 모두 만족할때에만 일어난다.

** future 객체는 async 호출에 의해 생성된 공유상태를 참조한다 **
** async 호출시 정해준 launch 옵션이 async 이다. **
** future 객체는 공유상태객체를 참조하는 마지막 future 객체이다. **

이것은 단지 표준의 선택일 뿐이며 암묵적 detach 를 수행했을 경우 최악의 상황에서는 프로그램 종료로 이어지며 이런 방침을 채용할순 없었기에 
암묵적 Join이라는 타협안을 선택했다.

async 로 실행되는 task 는 내부적으로 lock 를 건다든지 해서 공유메모리에 대해 접근순서 동기화를 해주는것 같다.  
atomic 나 semaphore 를 사용하지 않고 아무리 테스트를 해보아도 race condition 이 일어나지 않는다.
진짜 뭐냐 ?? 마법이야 ???
 
