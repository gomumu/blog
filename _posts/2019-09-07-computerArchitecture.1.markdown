---
layout: post
title:  "Chapter 1. Computer Abstractions and Technology(2)"
author: gomumu
categories: Computer_Architecture
---

<h2 id="headings">개요</h2>
<p>
목표 : 퍼포먼스의 정의를 이해 할 수 있다.<br>
강의 정보 : http://www.kocw.net/home/search/kemView.do?kemId=1125218<br>
</p>
<hr>

<h2 id="headings">전력의 경향</h2>
<p>
<img data-action="zoom" src='{{ "/assets/post/powerwall.jpg" | relative_url }}' > 
clock rate은 2004년도 까지 계속 증가해왔으나 2004년 이후로 clock Frequency는 정체되었다.<br>

$$ power = {CapacityLoad}\times{Voltage^2}\times{Frequency} $$
Voltage = 5v → 1v<br>
Frequency = x1000<br>
Power = x30<br>
칩의 전력 소모 공식을 사용하여 2004년의 전력 소모를 계산해보면 1982년보다 30배가 차이난다.<br>
전력 소모량이 계속 증가하자 clock Frequency는 더 이상 증가할 수 없게 되었다.<br>
</p>
<hr>

<h2 id="headings">전력 줄이기</h2>
<p>
새로운 CPU를 설계할 때 전력을 소모하기 위해 많은 노력을 한다.<br>
예를 들어 아래와 같이 디자인하여 전력 소모를 52퍼센트 정도 줄일 수 있다.<br>
<ul>
  <li>capacitive load = 이전 컴퓨터의 85%</li>
  <li>voltage = 15% 줄임</li>
  <li>frequency = 15% 줄임</li>
</ul>
$$ \frac{P_{old}}{P_{new}} = \frac{C_{old}\times{0.85}\times{(V_{old}\times{0.85})^2}\times{F_{old}}\times{0.85}}{C_{old}\times{(V_{old})^2}\times{F_{old}}} = {0.85}^4= 0.52 $$

<b>Power wall</b><br>
Power wall : 2004년 이후에 voltage를 더이상 낮출 수 없었으며 열 발생 문제를 해결할 수 없게 되었다. 때문에 더이상 Clock rate을 증가시킬 수 없었다.<br>
때문에 2004년 이후엔 전력 소모를 낮추기 위한 다른 방법을 사용하게 된다.<br>
</p>
<hr>


<h2 id="headings">Multiprocessors</h2>
<p>
하나의 칩이 여러개의 프로세서(Multi core)를 가지면서 성능 향상을 시킬 수 있었다.<br>
Multiprocessors 방식을 사용하면서 성능 개선률이 이전보다 줄긴 했는데 여러 제약 조건이 있기 때문이다.<br>
(power, instruction- level parallelism, memory latency)<br>

Multi core를 사용할 때는 sequencial 방식이 아닌 parallel programming을 사용해야 한다.<br>
parallel programming에는 두가지 방법이 있다.<br>
<ul>
  <li>instruction level parallelism : 하드웨어가 알아서 여러개의 명령어를 동시에 처리하는 방법</li>
  <li>parallel programming : 프로그래머가 일일이 짜는 방법</li>
</ul>
parallel programming을 직접 짜는 것은 로드밸런싱, communication, synchronization 오버헤드를 줄여야하는 문제가 있다.
</p>
<hr>

<h2 id="headings">Amdahl's Law</h2>
<p>
전체 시스템에서의 향상 수치는 전체 시스템에서 개선된 컴퍼넌트가 차지하는 부분의 비율에 비례해서 향상된다.<br>
$$T_{improved} = \frac{T_{affected}}{improvementFactor} + T_{unaffected} $$<br>
<b>Example</b><br>
곱하기 연산 전체연산 100초 중에 80초가 걸린다.<br>
곱하기 연산의 성능을 향상 시켜서 전체 성능을 5배 향상 시키려고 할때 곱하기 성능을 얼마나 향상시켜야할까? <br>
100/5 = 80/n + 20<br>
n = ∞ 이므로 곱하기 성능 개선만으로는 전체성능의 5%를 증가시키는 것은 불가능하다.<br><br>

<b>시스템 성능 향상하기 위해서는 시스템에서 가장 큰 비율을 가진 컴퍼넌트의 성능을 향상시키는 것이 가장 효과적이다.</b><br>
</p>
<hr>

<h2 id="headings">Low Power at Idle</h2>
<p>
<b>cpu 사용량이 적을 때 전력소모가 많이 줄진 않는다.</b><br>
<ul><b>인텔 I7의 경우</b>
  <li>100% CPU 사용 = 258W 의 전력소모</li>
  <li>50% CPU 사용 = 170W 의 전력소모</li>
  <li>10% CPU 사용 = 21W 의 전력소모</li>
</ul>
프로세서를 만들 때 load에 비례하도록 전력소모가 될 수 있도록 하는 것은 앞으로 중요한 문제가 될 것이다.<br>
</p>
