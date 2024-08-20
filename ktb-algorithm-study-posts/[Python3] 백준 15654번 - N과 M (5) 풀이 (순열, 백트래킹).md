<h1 id="📌-문제-정보">📌 문제 정보</h1>
<p>링크: <a href="https://www.acmicpc.net/problem/15654">https://www.acmicpc.net/problem/15654</a></p>
<p>유형: <code>순열</code>, <code>백트래킹</code></p>
<p>난이도: <code>실버3</code></p>
<p>스스로 풀었는가? ✅</p>
<br />

<hr />
<br />

<h1 id="💻-작성-코드">💻 작성 코드</h1>
<pre><code class="language-python">import sys

N, M = 0, 0
sequence = []
visited = []
answer = []

def back(cnt, start):
    global N, M, sequence, visited, answer

    if cnt == M:
        print(' '.join(map(str, answer)))

    for i in range(start, N):
        if not visited[i]:
            visited[i] = True
            answer.append(sequence[i])
            back(cnt + 1, i + 1)
            visited[i] = False
            answer.pop()

readline = sys.stdin.readline
N, M = map(int, readline().split())
sequence = list(map(int, readline().split()))
sequence.sort()
visited = [False] * N

if M == 1:
    output = '\n'.join(map(str, sequence))
    print(output)
else:
    back(0, 0)</code></pre>
<br />

<hr />
<br />

<h1 id="🎯-접근-방식">🎯 접근 방식</h1>
<ol>
<li><code>sort</code> 함수를 사용해 사전이 증가하는 순으로 수열을 정렬한다.</li>
<li>중복되는 수열을 여러 번 출력하면 안되며, 각 수열은 공백으로 구분해서 출력해야 한다.</li>
<li><code>itertools</code> 모듈의 <code>permutations</code> 함수를 이용해 N개의 자연수 중 길이가 M인 수열을 생성한다.</li>
<li>생성한 수열을 출력한다.</li>
</ol>
<br />

<hr />
<br />

<h1 id="💡-개선사항">💡 개선사항</h1>
<ol>
<li>백트래킹과 순열 함수를 모두 쓸 수 있는 경우에서는 함수를 쓰자. 실제로 방법1이 실행 속도가 더 빨랐다.</li>
</ol>
<br />

<hr />
<br />

<p>[ktb-algorithm-study] 2주차</p>