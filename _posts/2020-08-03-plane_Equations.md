 ---
layout: post
title: 평면의 방정식
subtitle: Plane Equations
gh-repo:
gh-badge: [star, fork, follow]
tags: [math]
comments: true
---

This is a demo post to show you how to write blog posts with markdown.  I strongly encourage you to [take 5 minutes to learn how to write in markdown](https://markdowntutorial.com/) - it'll teach you how to transform regular text into bold/italics/headings/tables/etc.


## 평면의 방정식

**평면을 정의하기 위해서는 다음 조건중 하나만 만족하면 된다.**
* 한 직선 위에 있지 않은 좌표가 3개 있다.
* 평면의 법선 벡터와 평면 위의 좌표가 하나 있다.

### 평면의 정의를 바탕으로 다음의 방정식을 사용한다.

a(x-x0) + b(y-y0) + c(z-z0) =0 

여기서 (a,b,c) 는 평면의 법선벡터이며
(x0,y0,z0)는 평면 상의 한 점을 의미한다.
(x,y,z)가 위 방정식을 만족하는 변수일때 (x,y,z) 는 평면 위의 좌표이다.

방정식의 값이 양수일때에는 평면의 
법선벡터 좌표의 내적의 결과가 0 ~ π/2 사이라는 의미이다. 
때문에 평면 안쪽에 존재한다고 해석하면 된다 (법선벡터가 가리키는 방향)
![plane2](/assets/_img/plane2.png)

이 앞뒤 판단은 카메라 뷰 프러스텀을 평면으로 구성한 이후에 컬링할때에 자주 사용된다.

![plane3](/assets/_img/plane3.png)

앞서 평면의 방정식을 언급하였는데 식을 전개하여서 간단히 만들어 보자. 
a(x-x0) + b(y-y0) + c(z-z0) =0 
= ax + by + cz + -ax0 -by0 - cz0 =0
= ax + by + cz  + ( (-ax0) +  (-by0)  + (-cz0) ) =0
여기서 (ax0 + by0 + cz0) 는 평면의 법선과 평면상의 존재하는 임의의 한점의 좌표의 내적과 같으며 내적의 결과 값을 d 라고 하였을때 최종적으로 일반화한 식은 다음과 같다.
~~~
 = ax + by + cz + d =0
~~~
d는 평면상의 한 점 아무거나 대입해서 방정식을 세워서 전개하면 쉽게 구할수 있다.
ax+by+cz = -d   여기서 x,y,z 는 평면상의 한 점

프로그래밍적으로 구현할때에는 무한 평면을 의미하는 노멀벡터와 평면상의 한점의 내적의 음수값을 -d 로 사용하면  x,y,z 를 매개변수를 받아와서 손쉽게 평면기준 위치를 구할 수 있다

{% highlight javascript linenos %}
float Collision_PlaneToPoint(vec3 n /*평면 법선*/,vec3 p/*평면위의 점*/,
vec3 pos /*구하고자 하는 점*/)
{
	// 원점과 평면과의 거리를 구한다.
	float d = 	-dot(n,p);
	// 클라이언트 코드에서 정의한 앱실론범위 이내라면 평면상의 점이다.
	return dot(n,pos) + d;
};
{% endhighlight %}



## Boxes
You can add notification, warning and error boxes like this:

### Notification

{: .box-note}
**Note:** This is a notification box.

### Warning

{: .box-warning}
**Warning:** This is a warning box.

### Error

{: .box-error}
**Error:** This is an error box.
