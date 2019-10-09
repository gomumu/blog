---
layout: post
title:  "연관 컨테이너(associative container)"
author: gomumu
categories: Algorithm
---

<h2 id="headings">연관 컨테이너(associative container)</h2>
<p>
개발을 하다보면 map, set이 자주 쓰이는데 실제 내부 구현 정확하게 몰라 정리하기 위해 포스팅을 하게 되었다.
사용법 보다는 내부 자료구조에 대해 비교하고 여러가지를 검증해보려고 한다.<br><br>
</p>
<hr>

<p>
<h3>map, muitimap</h3>
<b>map</b>은 '고유 키', '값'이 쌍으로 이루어진 연관 컨테이너이다. 키를 통해 정렬되며 일반적으로 레드 블랙 트리로 구현된다.
레드 블랙 트리는 균형 잡힌 이진 트리이며 삽입, 삭제 시에도 균형을 맞춰준다. 검색, 삽입, 삭제에 드는 시간은 $O(\log{n})$이다. 
<b>multimap</b>은 키가 중복 될 수 있으며 역시 레드블랙 트리로 구성된다.
</p><hr>

<p>
<h3>set, multiset</h3>
<b>set</b>은 키로 이루어진 연관 컨테이너이다. map과 마찬가지로 레드 블랙 트리로 구현된다.
<b>multiset</b>은 키가 중복 될 수 있으며 레드 블랙 트리로 구현된다.
</p><hr>

<p>
<h3>unordered_map, unordered_set</h3>
기존 map, set과 다른 점은 내부 구현이 해시로 정렬되어있다는 점이다. 때문에 정렬되어있는 상태가 아니며 해시 함수에 따라 정렬되어있다.
검색, 삽입, 삭제에 드는 시간은 상수 시간이다.
</p><hr>

<h3>map과 unordered_map의 속도 측정</h3>
<p>
x축 : data(개수)<br>
y축 : 시간(nano seconds)<br>
C++로 텍스트만 파일에 쓰고 그래프는 파이썬 plt를 이용하여 그렸다.<br>
코드는 "https://github.com/gomumu/Algorithm/associative container"에 있다.<br>

<img data-action="zoom" src='{{ "/assets/post/insert.PNG" | relative_url }}' >
삽입 시간은 다음과 같았다. 아마 해시 알고리즘이 레드블랙 트리를 구성하는 알고리즘보다 느린가보다.
<br><br>


<img data-action="zoom" src='{{ "/assets/post/find.PNG" | relative_url }}' >
탐색 시간은 다음과 같았다. 데이터가 적을때는 크게 차이 나지 않았지만 데이터 개수가 많아지니 점점 벌어진다. 레드블랙 트리도 빠르지만 데이터가 커질수록 상수시간에 수렴하는 해쉬가 빛을 발한다.
<br><br>

<img data-action="zoom" src='{{ "/assets/post/delete.PNG" | relative_url }}' >
삭제 시간이다. 탐색 후 삭제하기 때문에 해시가 빠를거라 생각했으나 거의 유사한 속도를 보여줬다.
아마 삭제 후에 해시 알고리즘과 레드 블랙 트리 구성 알고리즘에서도 차이가 있지 않을까 싶다.<br><br>

<b>결론</b><br>
1. 데이터가 왠만큼 많지 않은 이상 둘의 차이는 크지않다.<br>
2. 데이터 삽입 보다 데이터 검색 비중이 크다면 <b>unordered_map</b>을 고려하자.<br>
3. 데이터 삽입 보다 데이터 검색 비중이 작다면 <b>map</b>을 고려하자.<br>
</p>