<h1 id="📌-문제-정보">📌 문제 정보</h1>
<p>링크: <a href="https://www.acmicpc.net/problem/15657">https://www.acmicpc.net/problem/15657</a></p>
<p>유형: <code>백트래킹</code></p>
<p>난이도: <code>실버3</code></p>
<p>스스로 풀었는가? ✅</p>
<br />

<hr />
<br />


<h1 id="💻-작성-코드">💻 작성 코드</h1>
<pre><code class="language-python">import sys

N, M = 0, 0
sequence = []
answer = []

def back(cnt, start):
    global N, M, sequence, answer

    if cnt == M:
        print(' '.join(map(str, answer)))
        return

    for i in range(start, N):
        answer.append(sequence[i])
        back(cnt + 1, i)
        answer.pop()

readline = sys.stdin.readline
N, M = map(int, readline().split())
sequence = list(map(int, readline().split()))
sequence.sort()

back(0, 0)</code></pre>
<br />

<hr />
<br />

<h1 id="🎯-접근-방식">🎯 접근 방식</h1>
<ol>
<li>재귀 함수를 통해 길이가 M이 될 때까지 리스트에 값을 하나씩 추가한다.</li>
<li>값을 중복으로 포함할 수 있으므로 값이 현재 순열에 포함되어있는지 확인하지 않는다.</li>
<li>비내림차순으로 정렬되어야 하므로 start를 인자로 넘겨서 해당 값부터 반복문을 돈다.</li>
</ol>
<br />

<hr />
<br />

<h1 id="💡-개선사항">💡 개선사항</h1>
<ol>
<li><code>print(*answer)</code>으로 쉽게 정답을 출력할 수 있다.</li>
</ol>
<br />

<hr />
<br />


<p>[ktb-algorithm-study] 2주차</p>