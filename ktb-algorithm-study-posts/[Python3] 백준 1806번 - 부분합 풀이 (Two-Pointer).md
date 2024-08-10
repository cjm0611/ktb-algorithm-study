<h1 id="📌-문제-정보">📌 문제 정보</h1>
<p>링크: <a href="https://www.acmicpc.net/problem/1806">https://www.acmicpc.net/problem/1806</a></p>
<p>유형: <code>누적합</code>, <code>투포인터</code></p>
<p>난이도: <code>골드4</code></p>
<p>스스로 풀었는가? ✅</p>
<br />

<hr />
<br />


<h1 id="💻-작성-코드">💻 작성 코드</h1>
<pre><code class="language-python">import sys

readline = sys.stdin.readline
N, S = map(int, readline().split())
input_numbers = list(map(int, readline().split()))
accumulated_sum = [0] # 누적합
now_sum = 0
for number in input_numbers:
    now_sum += number
    accumulated_sum.append(now_sum)

start_idx = 0
end_idx = 0
min_length = sys.maxsize

while end_idx &lt;= N:
    temp_sum = accumulated_sum[end_idx] - accumulated_sum[start_idx]
    if temp_sum &lt; S:
        end_idx += 1
    elif temp_sum &gt; S:
        min_length = min(min_length, end_idx - start_idx)
        start_idx += 1
    else:
        min_length = min(min_length, end_idx - start_idx)
        end_idx += 1

if min_length == sys.maxsize:
    print(0)
else:
    print(min_length)</code></pre>
<br />

<hr />
<br />

<h1 id="🎯-접근-방식">🎯 접근 방식</h1>
<ol>
<li>부분합을 쉽게 구하기 위해 누적합 배열을 구한다. (0번째 index를 0으로 초기화하는 것 잊지 말자)</li>
<li><code>start_idx</code> 와 <code>end_idx</code> 를 왼쪽에서 시작하여 해당 범위의 누적합과 S를 비교해 포인터를 이동시킨다.</li>
<li>누적합이 S 이상이라면 <code>min_length</code> 와 비교해 작으면 업데이트한다.</li>
</ol>
<br />

<hr />
<br />

<h1 id="💡-개선사항">💡 개선사항</h1>
<ol>
<li>문제를 잘 읽자. <code>합이 S 이상이 되는 것 중 가장 짧은 것의 길이</code>에서 <code>이상</code> 이라는 키워드를 뒤늦게 발견했다.</li>
<li>찾아보니 슬라이딩 윈도우 기법을 사용하면 더 깔끔하게 풀 수 있다고 한다.</li>
</ol>
<br />

<hr />
<br />

<p>다른 방법으로는 <code>temp_sum</code>을 매번 계산하는 것이 아니라, while문 밖에 <code>sum</code> 변수를 하나 두고 idx가 움직일 때 변수의 값을 변경하는 방법이 있다.
하지만 기존 코드를 굳이 바꿀 필요는 없을 것 같다. 인덱스로 배열 값 가져오는 건 어차피 O(1)이니까.</p>
<p>[ktb-algorithm-study] 1주차</p>