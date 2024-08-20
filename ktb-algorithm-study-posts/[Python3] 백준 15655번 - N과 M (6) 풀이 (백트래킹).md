<h1 id="📌-문제-정보">📌 문제 정보</h1>
<p>링크: <a href="https://www.acmicpc.net/problem/15655">https://www.acmicpc.net/problem/15655</a></p>
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
<li>재귀 함수를 통해 길이가 M이 될 때까지 리스트에 값을 하나씩 추가한다. visited 배열을 통해 순열에 값이 중복 포함되지 않도록 한다.</li>
<li>start 값부터 for문을 돎으로써 순열이 오름차순이여야 한다는 조건을 만족한다.</li>
</ol>
<br />

<hr />
<br />

<h1 id="💡-개선사항">💡 개선사항</h1>
<ol>
<li>M이 1인 경우를 따로 별도로 처리할 필요가 없다.</li>
<li>visited 배열 대신 <code>if num in list:</code> 조건문을 통해 값이 중복으로 들어가지 않도록 한다. (코드가 짧아지고 메모리가 줄어드는 대신 실행 시간이 약간 증가)</li>
</ol>
<br />

<hr />
<br />

<p>풀이를 한번에 적으려니 기억이 안 난다.. 한 문제 풀 때마다 바로 풀이를 적는 게 편할 듯하다.</p>
<p>[ktb-algorithm-study] 2주차</p>