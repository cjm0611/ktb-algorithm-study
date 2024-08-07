<h1 id="📌-문제-정보">📌 문제 정보</h1>
<p>링크: <a href="https://www.acmicpc.net/problem/2230">https://www.acmicpc.net/problem/2230</a></p>
<p>유형: <code>정렬</code>, <code>투포인터</code></p>
<p>난이도: <code>골드5</code></p>
<p>스스로 풀었는가? ✅</p>
<br />

<hr />
<br />

<h1 id="💻-작성-코드">💻 작성 코드</h1>
<pre><code class="language-python">
import sys

readline = sys.stdin.readline

N, M = map(int, readline().split())
numbers = []
for i in range(N):
    numbers.append(int(readline()))

numbers.sort()

start_idx = 0
end_idx = 0
min_diff = sys.maxsize
while end_idx &lt; N:
    diff = numbers[end_idx] - numbers[start_idx]
    if diff == M:
        min_diff = min(min_diff, diff)
        end_idx += 1
    elif diff &gt; M:
        min_diff = min(min_diff, diff)
        start_idx += 1
    else:
        end_idx += 1

print(min_diff)
</code></pre>
<br />

<hr />
<br />


<h1 id="🎯-접근-방식">🎯 접근 방식</h1>
<ol>
<li>수열에서 두 수를 고르기만 하면 되므로 먼저 수열을 정렬한다.</li>
<li><code>차이(diff)</code>가 <code>목표값(M)</code>보다 크면 <code>start_idx</code> 늘리고, 목표보다 작으면 <code>end_idx</code> 늘리고, 목표와 같으면 <code>end_idx</code> 늘린다.</li>
<li><code>차이가 M 이상이면서 제일 작은 경우</code>를 구해야 하므로 <code>diff</code>가 <code>M</code> 이상이라면 <code>diff</code>와 <code>min_diff</code> 값을 비교한다.</li>
</ol>
<br />

<hr />
<br />

<h1 id="💡-개선사항">💡 개선사항</h1>
<ol>
<li>차이가 <code>M 이상이면서 제일 작은 경우</code>를 구하기 때문에, <code>diff == M</code>이라면 바로 반복문을 종료해도 된다.</li>
</ol>
<br />

<hr />
<br />


<p>[ktb-algorithm-study] 1주차</p>