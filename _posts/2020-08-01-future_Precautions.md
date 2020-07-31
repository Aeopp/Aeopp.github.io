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
그렇긴 한데 여기서 한가지 알아야 할 점이 있다. launch::async 로 policy 를 지정해서 future 객체를 얻었다면 해당 객체의 **소멸자가 wait 를 호출하기 때문이다.**
저기서 launch policy 를 매개변수로 받지 않는 오버로딩으로 호출하여도 컴파일러 제조사의 구현이 default policy가 async launch 라면 결과는 똑같을 것이다. (MSVC 는 async 인듯 결과 똑같은것 확인)
해결방법은 뭐 별 수 있나 future 를 제대로 받아서 라이프 사이클을 늘려야지 뭐

또한 async 로 실행되는 task 는 내부적으로 lock 를 건다든지 해서 공유메모리에 대해 접근순서 동기화를 해주는것 같다.  atomic 나 semaphore 를 사용하지 않아도 
race condition 이 일어나지 않는다....

신통방통하다 정말.... 테스트를 아무리 해보아도 race condition 이 일어나지 않는다.  솔직히 지금 심정은 마법을 쓰는것 같으며 머리속이 매우 복잡하다 어떻게 구현하였는지 힌트라도 누가 알려줬음 좋겠다....  

아직 갈길이 멀구나 ~ 
