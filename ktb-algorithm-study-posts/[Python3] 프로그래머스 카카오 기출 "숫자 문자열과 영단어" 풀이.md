<h1 id="📌-문제-정보">📌 문제 정보</h1>
<p>링크: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/81301">https://school.programmers.co.kr/learn/courses/30/lessons/81301</a></p>
<p>유형: <code>구현</code></p>
<p>난이도: <code>Lv.1</code></p>
<p>스스로 풀었는가? ✅</p>
<p>특이사항: 2021 카카오 채용연계형 인턴십 문제</p>
<br />

<hr />
<br />

<h1 id="💻-작성-코드">💻 작성 코드</h1>
<pre><code class="language-python">def solution(s):
    answer = s
    digit_eng_dict = {
        &quot;zero&quot;: 0,
        &quot;one&quot;: 1,
        &quot;two&quot;: 2,
        &quot;three&quot;: 3,
        &quot;four&quot;: 4,
        &quot;five&quot;: 5,
        &quot;six&quot;: 6,
        &quot;seven&quot;: 7,
        &quot;eight&quot;: 8,
        &quot;nine&quot;: 9
    }

    for key in digit_eng_dict.keys():
        answer = answer.replace(key, str(digit_eng_dict.get(key)))
    return int(answer)</code></pre>
<br />

<hr />
<br />

<h1 id="🎯-접근-방식">🎯 접근 방식</h1>
<ol>
<li>숫자와 영단어가 1대1로 대응되므로 dictionary를 이용한다.</li>
<li>dictionary를 순회하면서 replace method를 활용해 영단어를 숫자로 바꾼다.</li>
</ol>
<br />

<hr />
<br />


<h1 id="💡-개선사항">💡 개선사항</h1>
<ol>
<li><code>dict.keys()</code> 대신 <code>dict.items()</code>을 이용하면 쉽게 key와 value 값을 가져올 수 있다.</li>
<li>dictionary에 선언할 때부터 value를 str로 선언하면 형변환이 필요없다.</li>
</ol>
<br />

<hr />
<br />

<p>[ktb-algorithm-study] 1주차</p>