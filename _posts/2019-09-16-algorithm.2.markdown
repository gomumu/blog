---
layout: post
title:  "병합 정렬, 퀵정렬"
author: gomumu
categories: Algorithm
---
<h2 id="headings">개요</h2>
<p>
목표 : 고급 정렬에 대해 알아보자.<br>
참고 도서 : 문병로 『쉽게 배우는 알고리즘 관계 중심의 사고법』 한빛미디어<br>
예제 코드 : https://github.com/gomumu/Algorithm/sort
</p>
<hr>

<h2>병합 정렬(merge sort)</h2>
<p>
<img data-action="zoom" src='{{ "/assets/post/Merge-Sort-Steps.png" | relative_url }}' >
<b>아래 과정이 재귀적으로 동작한다.</b><br>
1. 입력을 반으로 나눈다.<br>
2. 전반부를 정렬한다.<br>
3. 후반부를 정렬한다.<br>
4. 전반부와 후반부를 병합하여 정렬한다.<br><br>

<b>점근적 분석</b><br>
병합 정렬의 점화식은 다음과 같다.<br>
$ T(n) = 2T(\frac{n}{2})+cn $<br>
마스터 정리를 이용하면 $\lim_{n\to\infty} {\frac{f(n)}{h(n)}} = {\frac{cn}{n^{\log_2{2}}}} = c$<br>
$c \in \Theta(1)$ 이므로 $T(n) = \Theta(n\log{n})$ 이다.<br>
</p>
<hr>

<h2>퀵 정렬(Bubble sort)</h2>
<p>
<img data-action="zoom" src='{{ "/assets/post/Quicksort.png" | relative_url }}' >
<b>아래 과정이 재귀적으로 동작한다.</b><br>
1. 피봇을 기준으로 피봇 왼쪽에는 피봇보다 작은 수 오른쪽에는 피봇보다 큰수로 나눈다.<br>
2. 피봇의 왼쪽 집합을 정렬한다.<br>
3. 피봇의 오른쪽 집합을 정렬한다.<br><br>

<b>점근적 분석</b><br>
퀵 정렬의 점화식을 최선/최악/평균으로 구해보자.<br>
※cn은 분할에 드는 비용<br><br>
<b>1. 피봇을 기준으로 반으로 나눠지는 경우</b><br>
$ T(n) = 2T(\frac{n}{2}) + cn $<br>
$\lim_{n\to\infty} {\frac{f(n)}{h(n)}} = {\frac{cn}{n^{\log_2{2}}}} = c$<br>
$c \in \Theta(1)$ 이므로 $T(n) = \Theta(n\log{n})$이다.<br><br>

<b>2. 피봇을 기준으로 한쪽에만 치우치는 경우</b><br>
$ \begin{align} T(n) & = T(n-1) + cn \\
& = T(n-2) + 2cn \\
& = T(n-3) + 3cn \\
& .........\\
& = T(1) + (n-1)\times{cn} \\
& ≤ c + (n-1)\times{cn} = cn^2 - cn + c \\
& \in = \theta(n^2)
\end{align} $<br><br>

<b>3. 나눴을 때 피봇의 위치가 i번째에 있는 경우</b><br>
$ T(n) = T(i-1) + T(n-i) + cn $<br>
$\frac{1}{n}\sum_{i=1}^{n} {(T(i-1) + T(n-i)) + cn}$<br>
$\frac{2}{n}\sum_{k=0}^{n-1} {(T(k)) + cn}$<br>
$T(n) = \theta(n\log{n})$<br>
</p>
<hr>



