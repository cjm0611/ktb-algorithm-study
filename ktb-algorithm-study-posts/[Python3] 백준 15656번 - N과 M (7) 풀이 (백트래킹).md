<h1 id="📌-문제-정보">📌 문제 정보</h1>
<p>링크: <a href="https://www.acmicpc.net/problem/15656">https://www.acmicpc.net/problem/15656</a></p>
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

def back(cnt):
    global N, M, sequence, visited, answer

    if cnt == M:
        print(' '.join(map(str, answer)))
        return

    for i in range(N):
        answer.append(sequence[i])
        back(cnt + 1)
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
    back(0)</code></pre>
<br />

<hr />
<br />

<h1 id="🎯-접근-방식">🎯 접근 방식</h1>
<ol>
<li>재귀 함수를 통해 길이가 M이 될 때까지 리스트에 값을 하나씩 추가한다.</li>
<li>값을 중복으로 포함할 수 있으므로 값이 현재 순열에 포함되어있는지 확인하지 않는다.</li>
</ol>
<br />

<hr />
<br />

<h1 id="💡-개선사항">💡 개선사항</h1>
<ol>
<li>M이 1인 경우를 따로 별도로 처리할 필요가 없다.</li>
<li>값이 중복으로 들어갈 수 있기 때문에 visited 배열은 사용하지 않는다. 코드 제출 전 꼼꼼하게 다시 확인하자.</li>
<li><code>print(*answer)</code>으로 쉽게 정답을 출력할 수 있다.</li>
</ol>
<br />

<hr />
<br />


<h1 id="💻-개선사항을-반영한-코드">💻 개선사항을 반영한 코드</h1>
<pre><code class="language-python">import sys

N, M = 0, 0
sequence = []
answer = []

def back(cnt):
    global N, M, sequence, answer

    if cnt == M:
        print(*answer)
        return

    for i in range(N):
        answer.append(sequence[i])
        back(cnt + 1)
        answer.pop()

readline = sys.stdin.readline
N, M = map(int, readline().split())
sequence = list(map(int, readline().split()))
sequence.sort()

back(0)</code></pre>
<br />

<hr />
<br />

<p>[ktb-algorithm-study] 2주차</p>