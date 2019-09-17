---
layout: post
title:  "병합 정렬, 퀵정렬, 힙정렬"
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

<h2>퀵 정렬(quick sort)</h2>
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

<h2>힙 정렬(heap sort)</h2>
<p>
힙이라는 특수한 자료구조를 사용하여 정렬하는 알고리즘이다.<br>
※힙은 이진 트리로서 맨 아래층을 제외하고 완전히 채워져 있고 맨 아래층은 왼쪽부터 채워져 있다.<br>

<img data-action="zoom" src='{{ "/assets/post/heapsort.png" | relative_url }}' >
<b>아래 과정이 재귀적으로 동작한다.</b><br>
1. 주어진 배열로 힙을 만든다.<br>
2. 힙에서 가장 작은 원소와 배열의 마지막 원소와 자리를 바꾼다.<br>
3. 배열에서 가장 작은 원소를 배제한다.
3. 위 과정을 반복한다.<br><br>

<b>점근적 분석</b><br>
힙 정렬의 시간은 힙의 높이에 비례한 시간이 걸린다.<br>
이진트리의 높이가 $\log_2{n}$이므로 heapify를 호출하는 시간은 $O(\log{n})$이 되며 buildHeap에서 heapify를 호출한 횟수는 $\frac{n}{2}$이기 때문에 $T(n) = O(n\log{n})$이다. 그러나 heapify를 $O(\log{n})$으로 잡는 것은 과하며 책에서는 엄밀히 계산하면 $\theta(n)$이 더 적합하다고 설명하고 있다. <br>
</p>
<hr>


