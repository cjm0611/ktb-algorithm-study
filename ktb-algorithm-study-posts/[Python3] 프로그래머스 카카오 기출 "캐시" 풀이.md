<h1 id="📌-문제-정보">📌 문제 정보</h1>
<p>링크: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/17680">https://school.programmers.co.kr/learn/courses/30/lessons/17680</a></p>
<p>유형: <code>구현</code></p>
<p>난이도: <code>Lv.2</code></p>
<p>스스로 풀었는가? ✅</p>
<p>특이사항: 2018 KAKAO BLIND RECRUITMENT 문제</p>
<br />

<hr />
<br />

<p>💻 작성 코드</p>
<pre><code class="language-python">def solution(cacheSize, cities):
    cities_in_cache = []
    total_time = 0
    CACHE_MISS_TIME = 5
    CACHE_HIT_TIME = 1

    if cacheSize == 0:
        total_time = len(cities) * CACHE_MISS_TIME
        return total_time

    for city in cities:
        city = city.lower()
        if city not in cities_in_cache:
            total_time += CACHE_MISS_TIME
            if len(cities_in_cache) &gt;= cacheSize:
                cities_in_cache.pop(0)
            cities_in_cache.append(city)
        else:
            total_time += CACHE_HIT_TIME
            cities_in_cache.remove(city)
            cities_in_cache.append(city)

    return total_time</code></pre>
<br />

<hr />
<br />


<h1 id="🎯-접근-방식">🎯 접근 방식</h1>
<ol>
<li>캐시된 도시를 담는 배열을 선언하여 입력으로 주어지는 도시를 배열에 추가한다. 인덱스 0번째의 도시가 항상 가장 오래 전에 캐시된 도시가 되도록 유지한다.</li>
<li>만약 이미 배열에 있다면, 가장 최근에 캐시된 도시라는 것을 나타내기 위해 캐시 배열에서 도시를 제거했다가 다시 추가한다.</li>
<li>배열에 없다면, 가장 오래 전에 캐시된 도시를 제거하고 새롭게 도시를 추가한다.</li>
</ol>
<br />

<hr />
<br />


<h1 id="💡-개선사항">💡 개선사항</h1>
<ol>
<li>deque의 maxlen을 cacheSize로 지정하면 사이즈를 초과하여 값이 추가될 때 자동으로 맨 앞의 값이 제거된다.</li>
</ol>
<br />

<hr />
<br />

<p>캐시 교체 알고리즘인 LRU를 기반으로 나온 문제라 좀 재밌었다.
캐시 알고리즘 복습해야겠다..
[ktb-algorithm-study] 2주차</p>