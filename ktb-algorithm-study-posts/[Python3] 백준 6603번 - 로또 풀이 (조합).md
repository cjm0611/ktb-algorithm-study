<h1 id="📌-문제-정보">📌 문제 정보</h1>
<p>링크: <a href="https://www.acmicpc.net/problem/6603">https://www.acmicpc.net/problem/6603</a></p>
<p>유형: <code>조합</code></p>
<p>난이도: <code>실버2</code></p>
<p>스스로 풀었는가? ✅</p>
<br />

<hr />
<br />


<h1 id="💻-작성-코드">💻 작성 코드</h1>
<pre><code class="language-python">import sys
from itertools import combinations

readline = sys.stdin.readline
input = readline().rstrip('\n')
while input != '0':
    arr = list(map(int, input.split()))
    k = arr[0]
    arr = arr[1:]
    LOTTO_LEN = 6
    combs = combinations(arr, LOTTO_LEN)
    for comb in combs:
        output = ' '.join(map(str, comb))
        print(output)
    print()
    input = readline().rstrip('\n')</code></pre>
<br />

<hr />
<br />

<h1 id="🎯-접근-방식">🎯 접근 방식</h1>
<ol>
<li>input으로 0이 들어올 때까지 반복적으로 배열을 입력 받는다.</li>
<li>배열에서 6인 조합들을 만들어 출력한다.</li>
</ol>
<br />

<hr />
<br />

<h1 id="💡-개선사항">💡 개선사항</h1>
<ol>
<li>변수를 한 줄에 할당할 수 있다. <code>k, numbers = arr[0], arr[1:]</code></li>
</ol>
<br />

<hr />
<br />

<p>이 문제를 풀면서 파이썬에는 do-while 문이 없다는 걸 알았다..</p>
<p>[ktb-algorithm-study] 2주차</p>