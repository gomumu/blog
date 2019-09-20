---
layout: post
title:  "기수 정렬, 계수 정렬"
author: gomumu
categories: Algorithm
---
<h2 id="headings">개요</h2>
<p>
목표 : 특수 정렬 알고리즘에 대해 알아보자.<br>
참고 도서 : 문병로 『쉽게 배우는 알고리즘 관계 중심의 사고법』 한빛미디어<br>
예제 코드 : https://github.com/gomumu/Algorithm/sort
</p>
<hr>

<h2>기수 정렬</h2>
<p>
<img data-action="zoom" src='{{ "/assets/post/radix_sort.jpg" | relative_url }}' >
입력 모두가 $k$ 이하의 자리수를 가진 순서가 있는 자료형(자연수, 알파벳 등)인 경우에 사용 할 수 있는 방법이다. 
 자리수 1부터 k까지 안정성을 유지하면서 정렬한다. 안정성을 유지한다는 것은 값이 같은 원소끼리는 정렬 후에 원래의 순서가 유지되는 성질을 말한다.<br><br>

<b>점근적 분석</b><br>
각 자리수를 정렬 하기 위해선 $O(n)$의 시간이 소요된다. 자리수만큼 곱해진다고 해도 자리수는 상수이므로 여전히 $O(n)$의 시간이 소요된다.
단 앞서 공부했던 정렬을 사용하면 $\theta(n)$의 시간을 초과하기 때문에 0~9까지의 저장 공간에 넣어놓고 나중에 차례로 배열을 만드는 방식으로 $O(n)$시간 안에 끝내야 한다.<br>
</p>
<hr>

<h2>계수 정렬</h2>
<p>
<img data-action="zoom" src='{{ "/assets/post/countingsort.gif" | relative_url }}' >
계수 정렬은 정렬 하고자 하는 원소들의 값이 $O(n)$을 넘지 않는 경우에 사용 할 수 있다.<br>
k 이하의 자연수를 가진 배열 A를 B에 정렬할 떄 아래 과정으로 동작한다.<br>
1. k 크기의 배열 C를 초기화한다.<br>
2. A를 순회하면서 C에서 각각의 값에 대한 카운팅을 한다.<br>
3. C에서 각각의 카운팅을 이전 위치의 값으로 누적시킨다.(순서를 정하기 위함)<br>
4. C에 기록되어 있는 순서를 이용하여 A에 있는 값을 B에 정렬시킨다.<br><br>

<b>점근적 분석</b><br>
위 4개의 반복문이 시간을 결정한다.<br>
1. $\theta(k)$<br>
2. $\theta(n)$<br>
3. $\theta(k)$<br>
4. $\theta(n)$<br>
k가 n이라면 총 시간은 $\theta(n)$의 시간이 걸린다.
</p>
<hr>
