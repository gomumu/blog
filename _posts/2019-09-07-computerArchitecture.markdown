---
layout: post
title:  "Chapter 1. Computer Abstractions and Technology"
author: gomumu
categories: Computer_Architecture
---

<h2 id="headings">개요</h2>
<p>
목표 : 퍼포먼스의 정의를 이해 할 수 있다.<br>
강의 정보 : http://www.kocw.net/home/search/kemView.do?kemId=1125218<br>
</p>
<hr>

<h2 id="headings">Performance</h2>
<p>
여러 종류의 비행기가 있다고 생각해보자. 비행기의 성능을 어떻게 비교할 수 있을까?<br>
<ul>
  <li>얼마나 많은 승객을 태울 수 있는지</li>
  <li>얼마나 멀리 갈 수 있는지</li>
  <li>얼마나 빨리 갈 수 있는지</li>
</ul>
성능은 보는 관점에 따라 달라질 수 있다. 어떤 비행기는 속도가 빠르며
어떤 비행기는 연비가 좋을 수 있으며 어떤 비행기는 많은 인원을 태울 수 있다.<br>
컴퓨터 분야에서도 여러 가지 관점에서 성능을 생각 할 수 있다.

<ul>
  <li>Response Time : operation에 걸리는 시간</li>
  <li>Throughput : 단위 시간당 얼마나 일을 할 수 있을지</li>
</ul>

만약 성능이 좋은 cpu로 바꾼 경우 Response time은 감소하고 Throughput은 증가한다.<br>
비슷한 예로 같은 성능의 cpu를 추가할 때 Response time은 그대로이며 Throughput은 증가한다.<br>
</p>
<hr>

<p>
<h2>기본 단위를 짚고가자.</h2>
<table cellspacing="0" cellpadding="0">
  <tr>
    <th>바이트</th><th>초</th><th>헤르츠</th>
  </tr>
  <tr>
    <td>$$ Byte = 8bit $$</td><td>$$ ms = 10^{-3} $$</td><td>$$ Hz = 10^{0} $$</td>
  </tr>
  <tr>
    <td>$$ KB = 2^{10} bytes $$</td><td>$$ µs = 10^{-6} $$</td><td>$$ kHz = 10^{3} $$</td>
  </tr>
  <tr>
    <td>$$ MB = 2^{20} bytes $$</td><td>$$ ns = 10^{-9} $$</td><td>$$ MHz = 10^{6} $$</td>
  </tr>
  <tr>
    <td>$$ MB = 2^{20} bytes $$</td><td>$$ ps = 10^{-12} $$</td><td>$$ GHz = 10^{9} $$</td>
  </tr>
  <tr>
    <td>$$ GB = 2^{30} bytes $$</td><td></td><td>$$ THz = 10^{12} $$</td>
  </tr>
  <tr>
    <td>$$ TB = 2^{40} bytes $$</td><td></td><td></td>
  </tr>
  <tr>
    <td>$$ PB = 2^{50} bytes $$</td><td></td><td></td>
  </tr>
  <tr>
    <td>$$ EB = 2^{60} bytes $$</td><td></td><td></td>
  </tr>
</table>
</p>
<br>


<h2 id="headings">CPU Clocking</h2>
<p>
clock : 컴퓨터 내부에서 CPU와 디지털 회로 장치들이 일정한 속도로 동기화 하여 작동하도록 발생시키는 정기적인 펄스<br>

$$ CC = \frac{1}{CR}$$

CC(Clock Period , clock cycle time) : 한 클락 사이클에 걸리는 시간<br>
CR(Clock Frequency(rate)) : 1 초당 클럭 사이클 수<br>
</p>
<hr>

<h2 id="headings">CPU Time</h2>
<p style="cambria_math">
CPU가 명령어를 처리할 때 걸리는 시간이다.<br>

$$ CPU Time = {CPU Clock Cycles}\times{CC} = \frac{CPU Clock Cycles}{CR}$$

<b>Example</b><br>
Computer A : 초당 2GHz, CPU Time : 10초 <br>
Designed Computer B : 같은 작업을 CPU Time 6초로 하고 싶어한다. 클락의 사이클 수는 A보다 1.2배 증가시키고 싶다.<br>
B의 초당 클락수(CR) 는?<br><br>

A : CR:2GHZ , CPU TIME:10초<br>
A : Total Cycles : 2 X 10^9 X 10 = 20 X 10^9<br>
B : CR:? , CPU TIME:6초<br>
B : Total Cycles : (20 X 10^9) X 1.2 = 24 X 10^9<br>
B : CR = 24 X 10^9 / 6초 = 4GHZ<br>
</p>
<hr>

<h2 id="headings">Instruction Count and CPI</h2>
<p>
총 클락 수(Clock Cycles)는 Instruction 수 X 하나의 Instruction당 걸리는 클락 수 (CPI) <br>

CPU TIME = Instruction 수 X 하나의 Instruction당 걸리는 클락 수 X Clock Cycle time <br>

$$ CPU Time = {Instruction count}\times{CPI} = \frac{CPU Clock Cycles}{CR}$$

CPI(Cycles per Instruction) : 인스트럭션의 클락 수

Instruction count는 프로그램, Instruction set Archictecture(ISA) 그리고 컴파일러에 영향을 받는다.<br>
CPI는 CPU 하드웨어가 어떻게 디자인 되었는지에 따라 결정된다.<br>

<br><b>Example</b><br>
Computer A : Cycle Time = 250ps, CPI = 2.0<br>
Computer B : Cycle Time = 500ps, CPI = 1.2<br>
which is faster, and by how much?<br>
Same ISA<br>
A 인스트럭션 시간 : 250 X 2.0 = 500 <br>
B 인스트럭션 시간 : 500 X 1.2 = 600 <br>
A가 1.2배 더 빠르다. <br>
</p>
<hr>

<h2 id="headings">CPI in More Detail</h2>
<p>
서로 다른 인스트럭션은 서로 다른 CPI를 가진다. 그렇기 때문에 여러 인스트럭션이 섞인 경우 평균 값으로 구한다. <br>
$$ Clock Cycles = \sum_{i=1}^{n} {CPI_i\times{InstructionCount_i}} $$
$$ CPI = \frac{Clock Cycles}{Instruction Count} = \sum_{i=1}^{n} ({CPI_i\times{\frac{InstructionCount}{InstructionCount_i}}}) $$

<br><b>Example</b><br>
다른 컴파일러로 컴파일된 코드 sequences1, sequences2가 있다. sequences1과 sequences2의 Avg.CPI를 구해보자.
<table cellspacing="0" cellpadding="0">
  <tr>
    <th>Class</th><th>CPI for class</th><th>IC in sqquence 1</th><th>IC in sqquence 2</th>
  </tr>
  <tr>
    <td>A</td><td>1</td><td>2</td><td>4</td>
  </tr>
  <tr>
    <td>B</td><td>2</td><td>1</td><td>1</td>
  </tr>
  <tr>
    <td>C</td><td>3</td><td>2</td><td>1</td>
  </tr>
</table>

sequences1 : ((1x2) + (2x1) + (3x2))/5 = 2<br>
sequences2 : ((1x4) + (2x1) + (3x1))/6 = 1.5<br>
</p>
<hr>

<h2 id="headings">Summary</h2>
<p>
$$ CPU Time = \frac{Instruction}{Program}\times\frac{ClockCycles}{Instruction}\times\frac{Seconds}{ClockCycle}$$
Program은 Instruction 으로 구성 되어있고<br>
Instruction은 Clock cycles로 구성되어있고<br>
Clock cycle은 Seconds로 구성되어있다.<br>

<b>퍼포먼스는 아래 항목에 영향을 받는다.</b>
<ul>
  <li>알고리즘 : IC, CPI에 영향을 줄 수 있다.</li>
  <li>프로그램 언어 : IC, CPI에 영향을 줄 수 있다.</li>
  <li>Compiler : IC, CPI에 영향을 줄 수 있다.</li>
  <li>ISA(Instruction Set Architecture) : IC, CPI , Clock Cycle Time에 영향을 줄 수 있다.</li>
</ul>
</p>
<hr>

<h2 id="headings">연습문제</h2>
<p>
<b>Moor's Law의 정의는?</b>
<details>
<summary>답</summary>
<p>매 2년마다 하나의 칩에 들어가는 트랜지스터의 수가 두배가 된다.</p>
</details>
<br><br>

<b>아래의 보기 중 성능이 향상되지 않는 경우는? (복수 선택 가능)</b><br>
<ol>
  <li>Throughput이 증가하는 경우</li>
  <li>Respose Time이 증가하는 경우</li>
  <li>Throughput이 감소하는 경우</li>
  <li>Respose Time이 감소하는 경우</li>
</ol>
<details>
<summary>답</summary>
<p>2, 3</p>
</details>
<br><br>

<b>표를 보고 아래 질문에 답해보자</b><br>
<table cellspacing="0" cellpadding="0">
  <tr>
    <th>$$ Op $$</th><th>$$ Freq $$</th><th>$$ CPI_i $$</th><th>$$ Freq\times{CPI_i} $$</th>
  </tr>
  <tr>
    <td>ALU</td><td>50%</td><td>1</td><td>0.5</td>
  </tr>
  <tr>
    <td>Load</td><td>20%</td><td>5</td><td>1</td>
  </tr>
  <tr>
    <td>Store</td><td>10%</td><td>3</td><td>0.3</td>
  </tr>
  <tr>
    <td>Branch</td><td>20%</td><td>2</td><td>0.4</td>
  </tr>
  <tr>
    <td></td><td></td><td></td><td>sum = 2.2</td>
  </tr>
</table>
Op : 명령어 종류<br>
Freq : 명령어 빈도<br>

<b>데이터 캐시를 사용하여 평균 load을 2사이클로 줄였을때 얼마나 향상되었는가?</b><br>
<details>
<summary>답</summary>
<p>
Load Clock Cycles 비율 = 0.2 x 2 = 0.4<br>
sum = 0.5 + 0.4 + 0.3 + 0.4 = 1.6<br>
향상 비율 = 2.2 / 1.6 = 1.375<br>
즉 37.5퍼센트 만큼 향상되었다.<br><br>
</p>
</details>
<br>

<b>브랜치 프레딕션 기법을 사용하여 Branch타입에서 걸리는 사이클 중 한 사이클 줄였을 때 얼마나 향상 되었는가?</b><br>
<details>
<summary>답</summary>
<p>
Branch Clock Cycles 비율 = 0.2 x 1 = 0.2<br>
sum = 0.5 + 1 + 0.3 + 0.2 = 2<br>
향상 비율 = 2.2 / 2 = 1.1<br>
즉 10퍼센트 만큼 향상되었다.<br><br>
</p>
</details>
<br>

<b>두개의 ALU 인스트럭션을 한번에 실행할때 얼마나 향상되는가?</b><br>
<details>
<summary>답</summary>
<p>
Branch Clock Cycles 비율 = 0.2 x 1 = 0.2<br>
sum = 0.5 + 1 + 0.3 + 0.2 = 2<br>
향상 비율 = 2.2 / 2 = 1.1<br>
즉 10퍼센트 만큼 향상되었다.<br><br>
</p>
</details>
<br>
</p>