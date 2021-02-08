---
layout: post
title: Navigation mesh
subtitle: Navigation mesh
tags: [Data Structure]
comments: true
---
# Navigation mesh
## 전략
* 네비게이션 메쉬는 삼각형 단위의 Segment 3개와 Point 3개로 구성하며 이것들을 Cell 이라고 앞으로 부른다.
* Cell은 이웃이 될 조건을 만족하는 다른 Cell들의 목록을 가지고 있으며 이것을 Neighbor 이라 부른다.
* 위의 이웃이 될 조건은 Point를 공유하면 만족하도록 한다.
* 네비게이션 메쉬의 통제를 받는 오브젝트는 특별한 경우가 아니면 Cell이 설치되지 않은 위치로 이동 할 수 없다. 
* Cell 내부에 존재하는지 아닌지는 Cell을 구성하는 선분 3개를 미리 2D 벡터로 구성 한뒤에 내적 연산으로 수행한다.
* Cell의 삼각형과 오브젝트가 충돌하는 경우 슬라이딩 벡터로 밀어준다.
