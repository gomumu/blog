---
layout: post
title:  "Chapter 2. Instructions: Language of the Computer(2)"
author: gomumu
categories: Computer_Architecture
---

<h2 id="headings">개요</h2>
<p>
목표 : Instructions을 이해 할 수 있다.<br>
강의 정보 : http://www.kocw.net/home/search/kemView.do?kemId=1125218<br>
참고 자료 : https://d4m0n.tistory.com/12
</p>
<hr>

<h2 id="headings">Arithmetic Operations</h2>
<p>

<b>C Code example</b>
{% highlight C++ %}
a = b+c;
{% endhighlight %}
<br>

<b>compiled MIPS code</b>
{% highlight C++ %}
add a, b, c  #temp a = b + c
{% endhighlight %}
<br>
<b>Design Principle 1: Simplicity favours regularity</b><br>
규칙성을 통해 간단하게 만드는게 좋다.<br>
규칙성을 주면 구현할 때 훨씬 수월하다.<br>
간단하게 만들어야 낮은 가격으로 하이 퍼포먼스가 가능하다.<br>
</p>
<hr>

<h2 id="headings">Register operands</h2>
<p>
CPU 내부의 있는 저장 공간이며 연산에 필요한 데이터를 저장한다.<br>
MIPS의 경우 32 bit(word) x 32 의 레지스터를 갖는다.<br>
앞서 보았던 MIPS operation - R-Type에서 레지스터 변수의 크기가 5 bit (0~31)인 이유는 레지스터의 인덱스를 가리키고 있기 때문이다.<br>
어셈블러에서 t로 시작하는 레지스터는 temlporary values이며 s로 시작하는 레지스터는 saved variable 이다.<br>

<b>Design Principle 2: Smaller is faster</b><br>
레지스터의 공간은 32개 이므로 데이터에 접근하는데 훨씬 빠르다.<br>
메모리의 공간은 수백만개이므로 훨씬 느리다.<br><br>

<b>Register Operand example</b><br>
<b>C Code</b>
{% highlight C++ %}
f = (g+h) - (i+j);
{% endhighlight %}
f...j = <b>$s0</b>...<b>$s4</b><br><br>

<b>compiled MIPS code</b>
{% highlight C++ %}
add $t0, $s1, $s2
add $t1, $s3, $s4
sub $s0, $t0, $t1
{% endhighlight %}
<br>
</p>
<hr>

<h2 id="headings">Memory Operands</h2>
<p>
산술 연산 시 레지스터에서 메모리 데이터를 로드하여 연산 후에 레지스터에 있는 값을 다시 메모리에 쓴다.<br>
메모리 주소는 바이트로 되어있으며 word단위로 데이터를 가져온다.<br>
때문에 메모리 주소는 4의 배수이다.<br>

<b>Memory Operand example</b><br>
<b>C Code</b>
{% highlight C++ %}
g = h + A[8];
{% endhighlight %}
<b>g</b> = <b>$s1</b><br>
A배열의 시작 주소 = <b>$s3</b><br><br>

<b>compiled MIPS code</b>
{% highlight C++ %}
lw  $t0, 32($s3)   #load word
add $s1, $s2, $t0
{% endhighlight %}
배열의 8번째 이므로 8x4 = 32번째 주소의 데이터를 로드(lw)한다.<br><br>

<b>Memory Operand example2</b><br>
<b>C Code</b>
{% highlight C++ %}
A[12] = h + A[8];
{% endhighlight %}

<b>h</b> = <b>$s2</b><br>
A배열의 시작 주소 = <b>$s3</b><br><br>

<b>compiled MIPS code</b><br>
{% highlight C++ %}
lw  $t0, 32($s3)   #load word
add $t0, $s2, $t0
sw  $t10,  48($s3) #store word
{% endhighlight %}
배열의 12번째에 주소의 데이터를 저장(sw)한다.<br>
</p>
<hr>

<h2 id="headings">Mips Register File</h2>
<p>
  <img data-action="zoom" src='{{ "/assets/post/mips-register.jpg" | relative_url }}' >
  레지스터의 개수가 32개이므로 Read포트에선 5bit를 받는다.<br>
  데이터의 입출력 시 데이터는 word단위이므로 32bit크기로 입출력한다.<br><br>

  Mips Register Convention<br>
  <img data-action="zoom" src='{{ "/assets/post/mips-register.gif" | relative_url }}' >
</p>
<hr>

<h2 id="headings">Immediate Operands</h2>
<p>
기존의 산술 연산과 달리 메모리 접근 없이 상수값을 가지는 경우이다.<br>
<b>compiled MIPS code</b><br>
{% highlight C++ %}
addi $s3, $s3, 4
{% endhighlight %}<br>

<b>Design Principle 3: Make the common case fast</b><br>
상수값을 메모리에서 로딩하는 것은 낭비이다.<br>
Immediate Operands는 load instruction의 수를 줄여준다.<br>
자주 사용되는 것을 빠르게 만들자<br>
</p>
<hr>

<h2 id="headings">The Constant Zero</h2>
<p>
move instruction을 구현 할 때 사용된다.<br>
<b>compiled MIPS code</b><br>
{% highlight C++ %}
add $t2, $s1, $zero
{% endhighlight %}
</p>
<hr>