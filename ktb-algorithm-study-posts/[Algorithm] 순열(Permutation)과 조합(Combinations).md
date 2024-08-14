<p>파이썬은 배열에서 순열과 조합을 구하는 라이브러리가 있다. ✨
구현이 어렵진 않지만 import문만 추가하면 간단하게 풀 수 있다.
상세 조건을 적용해 순열과 조합을 구해야 할 땐 백트래킹으로 구현해서 푼다.</p>
<br />

<h1 id="순열permutations">순열(Permutations)</h1>
<h2 id="정의">정의</h2>
<blockquote>
<p><strong>서로 다른 n개 원소에서 중복 없이, 순서를 고려해 r개의 원소를 선택해 나열하는 것</strong>
나열된 순서를 고려하기 때문에 <code>1 2</code>와 <code>2 1</code>을 다른 것으로 취급한다.</p>
</blockquote>
<p>예제 문제를 풀면서 순열을 어떻게 문제에 적용하는지 살펴보자.</p>
<br />

<h2 id="예제-백준-15654번-n과-m-5">(예제) 백준 15654번 &quot;N과 M (5)&quot;</h2>
<h3 id="문제-정보">문제 정보</h3>
<p>링크: <a href="https://www.acmicpc.net/problem/15654">https://www.acmicpc.net/problem/15654</a>
난이도: <code>실버 3</code></p>
<p>N개의 자연수 중에서 길이가 M개인 수열들을 구해 출력하는 문제이다.</p>
<br />

<h2 id="1-라이브러리-사용-python">1. 라이브러리 사용 (Python)</h2>
<pre><code class="language-python">import sys
from itertools import permutations

readline = sys.stdin.readline
N, M = map(int, readline().split())
sequence = list(map(int, readline().split()))
sequence.sort()

if M == 1:
    output = '\n'.join(map(str, sequence))
    print(output)
else:
    perms = permutations(sequence, M)
    for perm in perms:
        output = ' '.join(map(str, perm))
        print(output)</code></pre>
<ol>
<li><p>파이썬에서 자동으로 순열을 구해주는 라이브러리를 사용하기 위해 상단에 <code>from itertools import permutations</code>를 추가한다.</p>
</li>
<li><p><code>perms = permutations(sequence, M)</code>처럼 permutations 함수에 인자로 배열과 길이를 넘기면, 배열에서 만들 수 있는 길이 M의 모든 순열이 담긴 배열이 반환된다.</p>
</li>
</ol>
<blockquote>
<p>예를 들어 <code>permutations([1, 2, 3, 4], 2)</code> 은 길이가 2인 순열을 생성한다.</p>
<p>반환값: <code>[(1, 2), (1, 3), (1, 4), (2, 1), (2, 3), (2, 4), (3, 1), (3, 2), (3, 4), (4, 1), (4, 2), (4, 3)]</code></p>
</blockquote>
<br />

<h2 id="2-백트래킹으로-구현">2. 백트래킹으로 구현</h2>
<p>순열, 조합 문제 중에 조건이 복잡하여 라이브러리로 풀 수 없을 때 <strong>백트래킹</strong>을 이용해 구현할 수 있다.</p>
<h3 id="순열을-구하는-백트래킹-의사코드">순열을 구하는 백트래킹 의사코드</h3>
<pre><code class="language-python"># N개의 숫자와 M개의 선택된 숫자로 이루어진 순열을 생성하는 백트래킹 함수
백트래킹(현재 선택된 개수 cnt):
    만약 cnt가 M과 같다면:
        현재까지 선택된 숫자들을 출력
        반환

    # 가능한 모든 숫자를 탐색
    for i in 0에서 N-1까지:
        만약 i번째 숫자가 아직 선택되지 않았다면:
            i번째 숫자를 선택(방문 표시)
            현재까지 선택된 숫자들에 i번째 숫자를 추가
            백트래킹(cnt + 1)  # 다음 숫자를 선택하기 위해 재귀 호출
            i번째 숫자의 선택을 해제(방문 표시 해제)
            현재까지 선택된 숫자들에서 i번째 숫자를 제거  # 상태를 되돌림

# 초기 상태로부터 백트래킹 시작
백트래킹(0)
</code></pre>
<p>백트래킹의 핵심은 숫자를 선택해 추가한 후, 다음 상태로 이동해 모든 경우를 탐색하고, 탐색이 종료되면 선택한 숫자를 제거해 상태를 되돌려 탐색을 이어나가는 것이다. 이를 통해 가능한 수열의 모든 경우를 찾을 수 있다.
의사코드를 기반으로 python 코드를 작성해보자.</p>
<br />



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
        if not visited[i]:
            visited[i] = True
            answer.append(sequence[i])
            back(cnt + 1)
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
    back(0)</code></pre>
<h3 id="변수-설명">변수 설명</h3>
<p>N: 입력에서 주어지는 정수의 개수
M: 순열의 길이. 선택해야 할 숫자의 개수
sequence: 입력으로 주어지는 정수들의 리스트
visited: 배열의 각 요소가 순열에 선택된 상태인지를 나타내는 boolean 리스트로, 순열을 생성할 때 중복 선택을 방지하기 위해 사용된다.
answer: 현재까지 선택된 숫자들을 저장하는 리스트. M개의 숫자가 선택될 때까지 점점 채워지며, M개의 숫자가 모두 선택되면 answer에 담긴 숫자들을 출력한 후 상태를 되돌린다.</p>
<h3 id="함수-설명">함수 설명</h3>
<p>back(cnt): 백트래킹 함수. 현재까지 선택된 숫자의 개수(cnt)를 인자로 받는다. cnt가 M과 같아지면 현재까지 선택된 숫자들을 answer 리스트에서 출력한다. 재귀 호출이 끝나면 visited를 False로 바꾸고 answer에서 pop을 통해 선택된 숫자를 제거한다. 이후에 다시 탐색을 이어간다.</p>
<br />

<hr />
<br />

<h1 id="조합combinations">조합(Combinations)</h1>
<h2 id="정의-1">정의</h2>
<blockquote>
<p><strong>서로 다른 n개 원소에서 중복 없이, 순서를 고려하지 않고 r개의 원소를 선택하는 것</strong>
나열된 순서를 고려하지 않기 때문에 <code>1 2</code>와 <code>2 1</code>을 같은 것으로 취급한다.</p>
</blockquote>
<p>순서를 고려하지 않다는 차이점 빼고 순열과 동일하기에 자세한 설명은 생략한다.</p>
<br />

<blockquote>
<p><strong>라이브러리 이용</strong>
상단에 <code>from itertools import combinations</code>를 추가
<code>combs = combinations(arr, TARGET_LEN)</code> 처럼 정의함으로써 배열에서 원하는 길이로 조합된 수열 리스트를 구할 수 있다.</p>
</blockquote>
<p>예를 들어 <code>combinations([1, 2, 3, 4], 2)</code> 은 길이가 2인 순열을 생성한다. 
반환값: <code>[(1, 2), (1, 3), (1, 4), (2, 3), (2, 4), (3, 4)]</code></p>
<p>마찬가지로 백트래킹을 이용해 조합을 구현할 수 있다.</p>
<br />


<hr />
<br />


<p>[ktb-algorithm-study] 2주차</p>