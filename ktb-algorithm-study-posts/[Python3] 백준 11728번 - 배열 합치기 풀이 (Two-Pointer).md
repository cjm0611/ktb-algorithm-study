<h1 id="📌-문제-정보">📌 문제 정보</h1>
<p>링크: <a href="https://www.acmicpc.net/problem/11728">https://www.acmicpc.net/problem/11728</a></p>
<p>유형: <code>정렬</code>, <code>투포인터</code></p>
<p>난이도: <code>실버5</code></p>
<p>스스로 풀었는가? ✅</p>
<br />

<hr />
<br />

<h1 id="💻-작성-코드">💻 작성 코드</h1>
<pre><code class="language-python">import sys

readline = sys.stdin.readline

N, M = map(int, readline().split())
arr = list(map(int, readline().split()))
brr = list(map(int, readline().split()))

arr_idx = 0
brr_idx = 0
answer = []

while arr_idx &lt; len(arr) and brr_idx &lt; len(brr):
    a = arr[arr_idx]
    b = brr[brr_idx]
    if a &lt; b:
        answer.append(a)
        arr_idx += 1
    else:
        answer.append(b)
        brr_idx += 1

while arr_idx &lt; len(arr):
    answer.append(arr[arr_idx])
    arr_idx += 1

while brr_idx &lt; len(brr):
    answer.append(brr[brr_idx])
    brr_idx += 1

output = ' '.join(map(str, answer))
print(output)</code></pre>
<br />

<hr />
<br />

<h1 id="🎯-접근-방식">🎯 접근 방식</h1>
<ol>
<li>정렬된 두 배열을 합치려면 각 배열에 있는 값을 비교해야 하므로 투포인터를 이용한다.</li>
<li>포인터를 통해 배열을 순회하며 더 작은 값을 <code>answer</code>에 추가한다.</li>
<li>한 쪽 배열의 모든 값이 합쳐졌다면 다른 배열의 남은 값을 <code>answer</code>에 추가한다.</li>
</ol>
<br />


<hr />
<br />

<h1 id="💡-개선사항">💡 개선사항</h1>
<ol>
<li>list를 그대로 출력해서 한 번 틀렸다. 문제를 볼 때 Output을 잘 보자.</li>
<li>병합 이후에 남은 값들을 합칠 때 <code>answer.extend(arr[arr_idx:])</code> 를 통해 간단히 해결할 수 있다.</li>
</ol>
<br />

<hr />
<br />
[ktb-algorithm-study] 1주차