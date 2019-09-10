---
layout: post
title:  "점근적 분석 방법"
author: gomumu
categories: Algorithm
---
<h2 id="headings">개요</h2>
<p>
목표 : 점근적 분석 방법을 이해하고 구할 수 있다.<br>
참고 도서 : 문병로 『쉽게 배우는 알고리즘 관계 중심의 사고법』 한빛미디어
</p>
<hr>

<h2>점근적 표기의 종류</h2>
<p>
<h4>θ - 표기법</h4>
$$n^2 + 3 \in \Theta(n^2)$$
알고리즘의 소요시간이 입력의 크기 n에 대해 O(n^2)이라면 대략 n^2에 비례하는 시간이 소요됨을 나타낸다.
최고차항의 차수가 같은 함수들의 집합이다.<hr><br>

<h4>O - 표기법</h4>
$$2n + 3 \in O(n^2)$$
$$n^2 + 3 \in O(n^2)$$
알고리즘의 소요시간이 입력의 크기 n에 대해 O(n^2)이라면 기껏해야 n^2에 비례하는 시간이 소요됨을 나타낸다.
점근적 <b>상한</b>을 나타낸다.<hr><br>

<h4>Ω - 표기법</h4>
$$n^4 + 1 \in Ω(n^2)$$
$$n^2 + 3 \in Ω(n^2)$$
알고리즘의 소요시간이 입력의 크기 n에 대해 O(n^2)이라면 적어도 n^2에 비례하는 시간이 소요됨을 나타낸다.
점근적 <b>하한</b>을 나타낸다.<hr><br>
</p>

<h2>점화식의 점근적 분석 방법</h2>
<p>
<h4>반복대치</h4>
n이 1이 될때 까지 n을 n-1에 대치하여 점근적 복잡도를 구하는 방식이다.<br>
팩토리얼 함수를 반복 대치로 구해보자.<br>
{% highlight C++ %}
int factorial(int n) {
  if(n = 1) return 1; //...(c)
  return n*factorial(n-1); //...T(n-1)
}
{% endhighlight %}
factorial(n)를 반복대치를 이용하여 계산하면 아래와 같다.<br><br>
$ \begin{align} T(n) & = T(n-1) + c \\
& = T(n-2) + 2c \\
& = T(n-3) + 3c \\
& .........\\
& = T(1) + (n-1)\times{c} \\
& ≤ c + (n-1)\times{c} = cn \\
& \in O(n)
\end{align} $<br><br>

병합 정렬을 반복 대치로 구해보자.<br>
입력의 크기가 n인 배열에 대한 병합정렬을 할 때 총 대소 비교 횟수를 T(n)이라 하면 다음과 같다.<br><br>
$ T(n) ≤ 2T(\frac{n}{2})+n $
<br><br>
이것을 반복대치를 이용하여 풀어보면 다음과 같다.<br><br>
$ \begin{align} T(n) 
& ≤ 2T(\frac{n}{2}) + n \\
& ≤ 2(2T(\frac{n}{4}) + \frac{n}{2}) + n = 2^2T(\frac{n}{2^2}) + 2n \\
& ≤ 2^2(2T(\frac{n}{2^3} + \frac{2^2}{n}) + 2n = 2^{3}T(\frac{n}{2^3}) + 3n \\
& .........\\
& ≤ 2^kT(\frac{n}{2^K}) + kn \\
& ≤ nT(1) + kn = n + nlogn ...① \\
& \in O(nlog{n})
\end{align} $<br><br>
① 의 이유는 $\frac{n}{2^k} = 1$ 이라 할 때 $k = \log_2{n}$이 되기 때문이다.
</p>
<hr>

<h4>추정 후 증명</h4>
<p>
식의 모양을 보고 점근적 복잡도를 추정한 다음 그것이 옳음을 증명하는 방법이다.<br>
추정 후 증명법을 이용하여 병합정렬의 분석해보자.<br>

<fieldset>
$T(n) ≤ 2T(/frac{n}{2})+n$의 점근적 복잡도는 $T(n)=O(n\log{n})$이다.<br>
즉, 충분히 큰 n에 대하여 $T(n) ≤ cn\log{n}$인 양의 상수 c가 존재한다.<br>
</fieldset>

경계조건 : $T(2) ≤ c2\log{2}$ 를 만족하는 $c$가 존재한다. - (log 1 = 0 이므로 2를 경계조건으로 한다.)<br>
귀납적 가정과 전개 : $n$을 $\frac{n}{4}$로 가정해보면  $T(\frac{n}{4}) ≤ c\frac{n}{4}\log{\frac{n}{4}}$ 을 만족 해야한다.<br>

$ \begin{align} T(n) 
& ≤ 2T(\frac{n}{2}) + n \\
& ≤ 4T(\frac{n}{4}) + \frac{n}{2} \\
& = 4(c\frac{n}{4}\log{\frac{n}{4}}) + \frac{n}{2} \\
& = nc\log{\frac{n}{4}} + \frac{n}{2} \\
& = nc\log{n}-nc\log{4} + \frac{n}{2} \\
& = nc\log{n}+ n(\frac{1}{2}-c\log{4}) ... ①\\
& ≤ cn\log{n}
\end{align} $<br><br>
① 에서 c가 $\frac{1}{2^2}$이하이면 식을 만족하므로 증명이 완료된다.<br><br>
</p>
<hr>

<h4>마스터 정리</h4>
<p>
마스터 정리는 특정한 모양을 가진 재귀식에 대해 바로 결과를 알 수 있는 유용한 정리이다.<br>
마스터 정리는 다음과 같은 모양을 가진 식에 적용된다.<br>
$T(n)=aT(\frac{n}{b}) + f(n)$
즉 입력 크기 $n$인 문제를 풀기 위해선 입력 크기 $\frac{n}{b}$인 문제를 a개 풀고 나머지 $f(n)$의 오버헤드가 필요하다.<br>
병합 정렬이 대표적인 예로 $a=b=2, f(n)=n$인 경우다.

<b>마스터 정리 근사 버전</b><br>
<fieldset>
① $\lim_{n\to\infty} {\frac{f(n)}{h(n)}}=0$ 이면 $T(n)=\Theta(h(n))$이다.<br><br>
② $\lim_{n\to\infty} {\frac{f(n)}{h(n)}}=\infty$ 이고 충분히 큰 모든 $n$에 대해 $af(\frac{n}{b})<f(n)$이면 $T(n)=\Theta(f(n))$이다.<br><br>
③ $\lim_{n\to\infty} {\frac{f(n)}{h(n)}}=\Theta(1)$ 이면 $T(n)=\Theta(h(n)\log{n})$이다.<br>
</fieldset>
<br>
아래 내용과 같다.<br>
① $h(n)$이 더 무거우면 $h(n)$이 수행시간을 결정한다.<br>
② $f(n)$이 더 무거우면 $f(n)$이 수행시간을 결정한다.<br>
③ $h(n)$과 $f(n)$이 같은 무게이면 $h(n)$ (또는 $f(n)$)에 $\log{n}$을 곱한 것이 수행시간이 된다.<br>

책에선 마스터 정리의 원형과 정확히 같지 않음을 말하므로 유의해야한다.<br><br>
</p>
<hr>

<h4>마스터 정리를 이용하여 복잡도를 구해보자.</h4>
<p>
<fieldset>
$T(n)=2T(\frac{n}{3}) + c$ (c는 상수)
</fieldset>
$a=2$, $b=3$, $h(n)=n^{\log_{3}{2}}, f(n)=c$
$lim_{n\to\infty} {\frac{f(n)}{h(n)}} = lim_{n\to\infty} {\frac{c}{n\log_{3}{2}}}=0$ 이므로 마스터 정리 유형 ①에 해당된다.<br>
따라서 $T(n)=\Theta(n\log_{3}{2})$이다.<br><br><br>


<fieldset>
$T(n)=2T(\frac{n}{4}) + n$
</fieldset>
$a=2$, $b=4$, $h(n)=n^{\log_{4}{2}}=\sqrt{n}, f(n)=n$
$lim_{n\to\infty} {\frac{f(n)}{h(n)}} = lim_{n\to\infty} {\frac{n}{\sqrt{n}}}=\infty$ 이고 $af(\frac{n}{b}) = 2\times\frac{n}{4} = \frac{n}{2} < f(n)$이므로<br>
마스터 정리의 유형 ②에 해당된다.<br>
따라서 $T(n)=\Theta(n)$이다.<br><br><br>


<fieldset>
$T(n)=2T(\frac{n}{2}) + n$ (c는 상수)
</fieldset>
$a=2$, $b=2$, $h(n)=n^{\log_{2}{2}}, f(n)=n$
$lim_{n\to\infty} {\frac{f(n)}{h(n)}} = \Theta(1)$ 이므로 마스터 정리 유형 ③에 해당된다.<br>
</p>
<hr>
