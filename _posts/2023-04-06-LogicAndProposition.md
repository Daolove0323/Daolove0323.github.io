---
layout: single
categories:
  - DescreteMathematics
tags:
- DescreteMathematics
title: "논리와 명제"
comments: true
---



 논리적이라는 것은 주어진 문제를 객관적으로 명확하게, 그리고 사고의 법칙을 체계적으로 추구하여 분석하는지의 여부로 결정된다. 논리의 중요한 목적 중 하나는 특정 논리를 통한 입증이 옳은가를 측정하는데 필요한 법칙을 제공한다는 것이다.

 지금도 활발하게 진행되고 있는 논리에 대한 연구와 응용은 다른 연구 분야와 더불어 컴퓨터 관련 학문이나 공학 등 여러 분야에 폭넓게 응용되고 있다. 예를 들어, 알고리즘의 설계나 증명, 디지털 논리 회로의 설계, 논리 프로그램 관련 분야, 관계형 데이터베이스 이론, 오토마타와 계산 이론, 인공지능 등에 필요한 이론적 기반을 제공하고 있다.



## 논리와 명제

<hr/>

명제 논리(propositional logic) - 주어와 술어를 구분하지 않고 전체를 하나의 식으로 처리하여 참 또는 거짓을 판별하는 법칙

술어 논리(predicate logic) - 중어와 술어로 구분하여 참 또는 거짓을 판별하는 법칙

명제(proposition)란 참이나 거짓을 객관적으로 구분할 수 있는 문장이나 식

단순 명제(simple proposition) - 하나의 문장이나 식으로 구성되어 있는 명제

합성 명제(composition proposition) - 여러 개의 단순 명제들이 논리 연산자들로 연결되어 만들어진 명제

논리 연산자(logical operators) - 부정(~, not), 논리곱(^, and), 논리합(V, or), 배타적 논리합(+, exclusive or), 조건(->, if… then), 쌍방 조건(<-> if and only if(iff))

부정(negation) - 임의의 명제 p가 주어졌을 때, 그 명제에 대한 부종언 명제 p의 반대되는 진리값을 가지며, 기호로는 ~p라 쓰고 not p 또는 p가 아니다라고 읽는다.

진리표

p ~p

T F

F T

논리곱(conjunction) - 임의의 두 명제, p, q가 and로 연결되어 있을 때, 명제 p, q의 논리곱은 p^q라 쓰고, p and q 또는 p 그리고 q 라고 읽는다. 두 명제의 논리곱은 두 명제가 모두 참인 경우에만 참의 진리값을 가지고, 그렇지 않으면 거짓의 진리값을 가진다.

진리표

P q p^q

T T T

T F F

F T F

F F F

논리합(disjunction) - 임의의 두 명제 p, q가 or로 연결되어 있을 ㄷ때 두 명제 p, q의 논리합은 pVq라 쓰고, p or q라고 읽는다. 두 명제의 논리합은 두 명제가 모두 거짓인 경우에만 거짓의 지리값을 가지고, 그렇지 않으면 참의 진리값을 가진다.

배타적 논리합(exclusive or, xor) - 임의의 두 명제 p, q의 배타적 논리합은 p+q라 쓰고, exclusive or 또는 xor 이라고 읽는다. 배타적 논리합의 진리값은 p 와 q 두 명제 중에서 하나의 명제가 참이고 하나의 명제가 거짓일 때 참의 진리값을 가지고, 그렇지 않으면 거짓의 진리값을 가진다.

진리표

P q p+q

T t f

T f t

F t t

F f f

조건(implication) - 임의의 두명제 p,q의 조건 연산자는 p->q라쓰고, p이면 q이다. 라고 읽는다. 조건 연산자 p_>q는 p의 진리값이 참이고 q의 진리값이 거짓일 때만 거짓의 진리값을 가지고, 그렇지 않으면 참의 진리값을 가진다.

진리표

P q ->q

T t t

T f f

F t t

F f t

조건 연산자 ->는 p이면 q이다 뿐 아니라 다양한 표현이 가능하다.

P 이면 q이다.(if p, then q)

p는 q의 충분조건이다. (P is sufficient for q)

q는 p의 필요조건이다. (Q is necessary for p)

p는 q를 함축한다. (P implies q)

쌍방조건 - 임의의 두명제 p, q의 쌍방조건은 p<->q로 표시하고, p이면 q이고, q이면 p이다라고 읽는다. 쌍방조건의 진리값은 p,q가 모두 참이거나 거짓일 때 참의 진리값을 가지고, 그렇지 않으면 거짓의 진리값을 가진다.

진리표

P q p<-q

T t t

T f f

F t f

F f t

쌍방조건의 다른 표현

p이면 q이고 q이면 p이다. (P if and only if q)

p는 q의 필요충분조건이다. (P is necessary and sufficient for q)

합성명제의 연산자 우선순위

~ ^ V -> <->

명제 p->q에 대하여 q->p를 역(converse)

~p -> ~q를 이(inverse)

~q -> ~p를 대우(contrapositive) 라 한다.

이때 명제와 그의 대우는 논리적 동치 관계이다.

역과 이는 대우 관계이다.

항진 명제(tautology) - 합성 명제에서 그 명제를 구성하는 단순명제들의 진리값에 관계없이 그 합성명제의 진리 값이 항상 참인 명제

모순 명제(contradiction) - 합성 명제에서 그 명제를 구성하는 단순 명제들의 진리값에 관계없이 그 합성 명제의 진리 값이 항상 거짓인 명제

두 명제 p, q의 쌍방 조건 p<->q가 항진 명제라면, 두명제는 논리적 동치(logical equivalence)이며 p (=세개) q 또는 p (이상한 화살표)q라 적는다.

논리적 동치관계의 기본법칙

책 63p

추론(argument) - 주어진 명제가 참인 것을 바탕으로 새로운 명제가 참외 되는 것을 유도해내는 방법

유효 추론(valid argument) - 주어진 전제가 참이고 결론도 참인 추론

허위 추론(fallacious argument) - 추론이 거짓

전제(premise)를 p1, p2, p3 … pn이라하고 결론을(conclusion) q라 할 때 p1, p2, p3 … pn ㅏ q라 적는다.

여러가지 추론법칙

P66

술어논리

명제 중에서 변수가 있어 참과 거짓을 판단하기 힘든 경우가 있다. 이와 같은 형태의 명제를 p(x)라 적고, p(x)를 변수 x에 대한 명제 술어(propositional predicate)라 한다. 명제논리와 구분하여 명제 술어에 대한 논리를 술어 논리(predicate logic)라고 한다.

술어 한정자(predicate quantifier) - 술어를 나타내는 방법 중 변수의 범위를 한정시키는 방법

For all 과 there exist, a ,e 가 있다.

전체한정자(universal quantifier), a

존재 한정자(existential quantifier), e

~(a x p(x)) <-> ex(~p(x))

모든 x에 대하여 p(x)가 성립한다의 부정은

p(x)가 성립하지 않는 x가 존재한다 이다.

~(e x p(x)) <-> a x(~p(x))

p(x)가 성립하는 x가 존재한다의 부정은

모든 x에 대해 p(x)가 성립하지 않는다 이다.