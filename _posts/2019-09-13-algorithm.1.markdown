---
layout: post
title:  "선택 정렬, 병합 정렬, 삽입 정렬"
author: gomumu
categories: Algorithm
---
<h2 id="headings">개요</h2>
<p>
목표 : 기본적인 정렬에 대해 알아보자.<br>
참고 도서 : 문병로 『쉽게 배우는 알고리즘 관계 중심의 사고법』 한빛미디어<br>
예제 코드 : https://github.com/gomumu/Algorithm/sort
</p>
<hr>

<h2>선택 정렬(selection sort)</h2>
<p>
<img data-action="zoom" src='{{ "/assets/post/selectionsort.png" | relative_url }}' >
1. 배열 A의 범위[1, n]에서 가장 큰 원소를 찾아 이 원소의 배열 맨 끝으로 옮긴다<br>
2. 배열 A의 범위[1, (n-1)]에서 큰 원소를 찾아 이 원소의 배열 맨 끝으로 옮긴다<br>
3. 배열 A의 범위[1, (n-2)]에서 큰 원소를 찾아 이 원소의 배열 맨 끝으로 옮긴다<br>
4. 배열 A의 범위가[1, 1]을 수행 할 떄 까지 가장 큰 원소를 끝으로 옮긴다.<br><br>

<b>점근적 분석</b><br>
선택 정렬에서 대소를 비교하는 횟수는 다음과 같다.<br>
$\sum_{k=n}^{1} {(n-1)}$
$ = (n-1) + (n-2) + (n-3) + ... (1-1) = \frac{n(n-2)}{2}$<br>
$\frac{n(n-2)}{2}$의 점근적 복잡도는 $\theta(n^2)$이므로 수행시간은 $\theta(n^2)$ 이다.<br>
</p>
<hr>

<h2>병합 정렬(selection sort)</h2>
<p>
<img data-action="zoom" src='{{ "/assets/post/BubbleSort.png" | relative_url }}' >
1. 배열 A의 범위[1,n) 원소들을 차례로 현재 위치의 다음 원소와 비교하여 큰 경우 자리를 바꾼다. <br>
2. 배열 A의 범위[1,(n-1)) 원소들을 차례로 현재 위치의 다음 원소와 비교하여 큰 경우 자리를 바꾼다. <br>
3. 배열 A의 범위[1,(n-2)) 원소들을 차례로 현재 위치의 다음 원소와 비교하여 큰 경우 자리를 바꾼다. <br>
4. 배열 A의 범위가[1, 2)을 수행 할 때 까지 자리를 바꾼다.<br><br>

<b>점근적 분석</b><br>
버블 정렬에서 원소들을 순환하는 횟수는 다음과 같다.<br>
$\sum_{k=n}^{2} {(n-1)}$
$ = (n-1) + (n-2) + (n-3) + ... (2-1) = \frac{n(n-1)}{2}$<br>
$\frac{n(n-1)}{2}$의 점근적 복잡도는 $\theta(n^2)$이므로 수행시간은 $\theta(n^2)$ 이다.<br>
</p>
<hr>

<h2>삽입 정렬(insertion sort)</h2>
<p>
<img data-action="zoom" src='{{ "/assets/post/insertionsort.png" | relative_url }}' >
1. 배열 A의 범위[1,n]의 원소들을 차례로 이전 원소(k)와 비교하여 알맞은 위치에 삽입하고 다른 원소들의 인덱스를 바꿔준다.<br><br>

<b>점근적 분석</b><br>
만약 같은 방식으로 정렬이 되어있다면 현재 위치에 그대로 넣기만 하면 되기 때문에 순환 횟수는 $n$이므로 $Ω(n)$이다. 그러나 내림 차순으로 정렬되어있는 배열을 다시 오름차순으로 정렬하기 위해 삽입정렬을 사용하면 아래와 같이 계산된다.<br>

$\sum_{k=1}^{n} {(n-1)}$  
$ = (1-1) + (2-1) + ... + (n-2) + (n-1) = \frac{n(n-1)}{2}$<br>
$\frac{n(n-1)}{2}$의 점근적 복잡도는 $\theta(n^2)$이므로 수행시간은 $O(n^2)$ 이다.<br>
</p>
<hr>


