---
layout: post
title: 일반 삼각형의 사인 법칙
subtitle: law of sines of common triangle
gh-repo:
gh-badge: [star, fork, follow]
tags: [math]
comments: true
---

# 일반 삼각형에서의 사인과 코사인

## 일반 삼각형의 사인 법칙
**일반 삼각형에서 각 변의 길이와 마주 보는 각의 크기에 대한 사인 값에 대하여 다음과 같은 관계가 성립한다.**

![picture0](/assets/img/Triangle1.png)

	a/sin(α) = b/sin(β) = c/sin(γ) 
	
![picture1](/assets/img/sine_law.png)

왜 이런 관계가 성립하는지는 삼각형의 넓이를 통한 증명을 통해 알 수 있다.

해당 삼각형의 넓이는 *½ch* 이다.
삼각법에 따르면 h = b sin(A) 이며 삼각형 ABC 의 넓이 K는 다음과 같다.

	K = 1/2ch = 1/2bc sin(A)
	2K = bc sin (A) = ac sin (B) = ab sin(C)
	여기서 abc 로 각 항을 나눠주자.
	bc sin (A) / abc = ac sin(B) / abc  = ab sin(C) / abc
	= sin(A) / a = sin(B) / b  = sin(C) / c 

이 법칙은 다음과 같이 표현 할 수도 있다.
두 변의 길이의 비는 각 변과 마주 보는 각의 크기에 대한 사인값의 비와 같다.

그 이유는 곱셈법칙으로 쉽게 알 수 있다.

	a/sin(α) = b/sin(β) <=> a = b sin(α) / sin(β)  <=> a/b = sin(α)/sin(β)
이를 다른 변의 길이와 마주 보는 각의 크기의 비에 적용하면 똑같은 결과를 얻는다.
	
	a/b = sin(α)/sin(β)
	b/c = sin(β)/sin(γ)
	a/c = sin(α)/sin(γ)

![picture2](/assets/img/Triangle2.png)


해당 삼각형에서 두 각과 두 각 사이의 선분의 길이를 알고있다. 여기서 x의 길이를 앞에서 배운 법칙을 사용해 구해보자. 

먼저 삼각형의 두 각을 알고 있으니 나머지 한 각은 손쉽게 구해진다. 

	γ = 180 - 43 - 58 = 79

이제 앞서 배운 법칙을 사용하자.

	case a : x / 15 = sin(43) / sin(79)  <=>  x =  15 sin(43) / sin(79) = 10.42
	case b : x / sin(43) = 15 / sin(79) <=> x = 15 sin(43) / sin(79) = 10.42

