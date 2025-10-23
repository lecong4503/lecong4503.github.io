---
layout: post
title: 조합회로, 왜 중요한가?
date: 2025-10-22 18:00:00 +0900
categories: 디지털 설계
tags: 기본 개념
toc: true
---

## 0. Intro
조합회로는 디지털 논리회로의 가장 기본적인 요소이다.


하지만 '기본'이라는 말이 '중요하지 않다'는 뜻은 아니다.


오히려 칩의 성능과 효율을 결정하는 가장 핵심적인 열쇠는 바로 조합회로에 있다.


이번 글에서는 그 두 가지 이유를 자세히 살펴보겠다.



## 1. 모든 계산은 조합회로에서 수행한다.
순차회로가 데이터를 기억하고 전달한다면, 조합회로는 그 데이터로 실제 계산을 수행한다.

● 간단한 예제

간단한 예제로 그림 1 카운터를 보도록 하자

![그림 1. counter](/assets/images/digital_logic/counter_update.png)

``` verilog
always @ (posedge clk) begin
	...
    count <= count + 1;
end
``` 

여기서 '+1' 을 하는건 Adder 즉, 조합회로다.

@ (posedge clk) 와 <= 는 순차회로 요소이지만, 실제 더하기 라는 연산은 조합회로에서 담당한다.


순차회로는 위 코드에서 결과를 저장하는 역할만 할 뿐이다.

## 2. 칩의 속도는 조합회로가 결정한다.
칩의 최대 동작 주파수는 

가장 긴 조합회로 경로(Critical Path)에 의해 결정된다.

    Critical Path : 레지스터에서 나온 신호 혹은 입력된 신호가 조합회로를 거쳐 다음 레지스터에 안정적으로 입력되기까지의 경로


![그림 2. Critical Path](/assets/images/digital_logic/critical_path_up.png)
 

실제 회로 설계에서는 조합회로와 순차회로를 거의 항상 함께 사용한다.

앞서 설명했듯이 조합회로는 계산, 순차회로는 저장을 담당한다.

각각 따로 쓸 수는 있지만, 정확한 동작을 위해서는 같이 써야 한다.

 

조합회로만 있으면? 계산은 되지만 데이터가 언제 나올지 알 수 없어서 불안정하다.

순차회로만 있으면? 값을 저장하고 출력은 되지만 계산을 못 한다. 그래서 둘 다 필요하다.

 

그렇다면 왜 조합회로가 칩의 속도를 결정할까?

순차회로는 clock edge를 감지하여 데이터를 저장하고 출력한다.

이때 clock edge가 감지되었는데도 조합회로의 critical path가 너무 길어서 계산이 다 이루어지지 않았다면, 잘못된 값이 저장되고 출력된다.

이를 방지하려면 조합회로가 계산을 끝내는 시간에 맞춰 clock frequency를 설정해야 한다.

    critical path = 15ns → 최대 약 66MHz
    critical path = 10ns → 최대 약 100MHz
 

critical path가 길어질수록 clock frequency를 느리게 잡아야 하고, 결국 칩 전체의 속도가 느려진다.

 

그렇다면 이 critical path가 길어지는 문제를 어떻게 해결할까?

정답은 critical path의 사이사이에 순차회로인 register를 넣어주는 pipelining을 사용하는것이다.

 

예시로 다음 그림 3과 같은 순차회로와 조합회로로 이루어진 회로가 있다고 할 때,


![그림 3. Pipelining 적용 전](/assets/images/digital_logic/critical_path_01_up.png)
 

조합회로들의 데이터 처리 시간을 계산하면 총 13ns가 걸린다.

critical path가 13ns라는 것이다.
이렇게 되면 순차회로인 register에서 값을 캐치하려면 clock edge가 13ns 주기로 즉, 76.9MHz 로 동작해야한다.


![그림 4. Pipelining 적용 후](/assets/images/digital_logic/critical_pipe_up.png)
 

그림 4 처럼 register를 조합회로 사이에 넣어주는 간단한 조치만으로 critical path가 13ns에서 8ns로 줄었다.
이렇게 되면 clock frequency를 76.9MHz 에서 8ns 주기인 125MHz로 상승시킬 수 있게 되면서 전체 칩 속도가 향상된다.

 

다만, pipelining을 적용하면 최종 계산 결과가 나오기까지 그림 3에서 걸린 1 클럭보다 늘어난 2 클럭이 걸리게 되어 지연시간(Latency)가 늘어난다는 단점이 있다.

하지만 clock frequency 자체를 높일 수 있어 단위 시간당 더 많은 데이터를 처리할 수 있는 처리율(Throughput)은 월등히 높아진다. 회로설계시 이 Latency와 Throughput 사이의 Trade-off를 고려하여 최적의 pipeline을 결정해야 한다.

 

이렇게 조합회로의 critical path를 어떻게 관리해주느냐에 따라 칩의 속도가 결정된다.

## 3. 정리
지금까지 조합회로가 왜 중요한지 두 가지 관점에서 살펴봤다.

모든 계산은 조합회로에서 수행한다.
  더하기, 곱하기, 비교 등 모든 연산
  시스템의 기능을 결정하는 곳

칩의 속도는 조합회로가 결정 
  critical path가 최대 동작 주파수 결정
  pipelining으로 속도 향상 가능

교과서에서는 조합회로를 "출력이 현재 입력에만 의존하는 회로"라고 정의한다.

맞는 말이다.

하지만 실제로 설계하다 보면 이 정의 만으로는 부족하다는 걸 느낀다.

 

석사 기간 AI 가속기를 설계할 때,

곱셈기 하나를 최적화하느라 많은 시간동안 고민했다.

 

Wallace Tree를 쓸까, Dadda Tree를 쓸까.

몇 stage로 나눌까. 어디에 Register를 넣을까.

 

조합회로의 지연 특성을 파악하고,

최적의 분할점을 찾는 과정이

결국 조합회로를 얼마나 깊이 이해하느냐에 달려있었다.

 

그래서 회로 설계를 공부한다는 건

결국 조합회로를 제대로 이해하는 것부터 시작한다고 생각한다.
