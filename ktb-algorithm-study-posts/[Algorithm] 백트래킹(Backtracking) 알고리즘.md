<h1 id="백트래킹이란">백트래킹이란?</h1>
<p>백트래킹은 완전 탐색 알고리즘의 일종으로, <code>재귀</code>를 기반으로 해를 찾는 도중에 해가 아니라고 판단되는 경우 돌아가서 다른 경로를 탐색하는 방식이다. 모든 가능한 경우의 수를 탐색하면서 조건에 맞는 해를 찾지만, 중간에 해당 상태는 정답에 도달할 수 없다고 판단되면 해당 노드부터 하위의 노드를 탐색하지 않는다.</p>
<blockquote>
<p>가능한 모든 경우의 수를 탐색하되 정답 가능성이 없는 경로는 더 이상 탐색하지 않고 되돌아간다.</p>
</blockquote>
<br />



<h2 id="순열을-구하는-백트래킹-의사코드">순열을 구하는 백트래킹 의사코드</h2>
<p><a href="https://velog.io/@cjm-0611/Algorithm-Recursion-Basic-%EC%88%9C%EC%97%B4Permutation-%EC%A1%B0%ED%95%A9Combinations">순열과 조합 알고리즘</a>을 다루면서 백트래킹에 대해 소개한 적이 있다.</p>
<pre><code class="language-python"># N개의 숫자와 M개의 선택된 숫자로 이루어진 순열을 생성하는 백트래킹 함수
백트래킹(현재 선택된 개수 cnt):
    만약 cnt가 M과 같다면: # 기저 조건 - 순열의 길이가 M
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
백트래킹(0)</code></pre>
<p><code>기저 조건(base condition)</code>은 재귀 함수에서 더 이상 재귀적으로 호출하지 않고, 즉시 결과를 반환하거나 특정 작업을 수행하는 조건을 말한다. 목표로 하는 상태, 정답에 도달한 경우에는 탐색을 이어갈 필요가 없으므로 종료한다.</p>
<p>위 의사코드의 핵심은 숫자를 선택해 추가한 후, 다음 상태로 이동해 모든 경우를 탐색하고, 탐색이 종료되면 선택한 숫자를 제거해 상태를 되돌려 탐색을 이어나가는 것이다. 이를 통해 가능한 수열의 모든 경우를 찾을 수 있다.</p>
 <br />


<h2 id="체스-퀸-문제-n-queens-문제">체스 퀸 문제: N-Queens 문제</h2>
<p>체스 퀸 문제는 대표적인 백트래킹 문제로, N x N 체스판 위에 N개의 퀸을 서로 공격하지 않도록 배치하는 문제이다. 퀸은 같은 행, 열, 대각선에 위치한 다른 퀸을 공격할 수 있기 때문에 N개의 퀸이 서로를 공격하지 않도록 N개의 서로 다른 행에 배치하는 방법을 찾는 문제이다.</p>
<pre><code class="language-python">boardSize = int(input())
queens = []
answer = 0
columns = [False] * boardSize

def can_put_chess(now_i, now_j):
    for queen in queens:
        i, j = queen
        diff_i = abs(now_i - i)
        diff_j = abs(now_j - j)
        if diff_i == diff_j:
            return False

    return True

def put_chess(row):
    global answer, queens
    if row ==  boardSize: # 기저 조건 - 모든 퀸을 배치한 경우
        answer += 1
        return

    for j in range(boardSize):
        if not columns[j] and can_put_chess(row, j): # 해당 열에 퀸을 배치할 수 없다면 다음 열을 탐색하게 됨
            queens.append((row, j))
            columns[j] = True
            put_chess(row + 1)
            queens.remove((row, j)) # 다른 경우를 탐색하기 위함
            columns[j] = False

put_chess(0)
print(answer)</code></pre>
<p>이 코드는 퀸을 체스판의 각 행에 하나씩 놓으면서 다음 행으로 이동하여 계속 놓을 수 있는지 탐색한다. 충돌이 발생하면, 해당 위치는 놓을 수 없으므로 이전 단계로 돌아가 다른 가능성을 탐색하는 과정을 반복한다. 가능한 모든 경우를 시도하면서 유효하지 않은 경우를 빠르게 배제할 수 있다.</p>
<br />

<hr />
<br />
[ktb-algorithm-study] 3주차