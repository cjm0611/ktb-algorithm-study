<h1 id="📌-문제-정보">📌 문제 정보</h1>
<p>링크: <a href="https://www.acmicpc.net/problem/17609">https://www.acmicpc.net/problem/17609</a></p>
<p>유형: <code>문자열</code>, <code>투포인터</code></p>
<p>난이도: <code>골드5</code></p>
<p>스스로 풀었는가? ❌ (질문 게시판 이용)</p>
<br />

<hr />
<br />


<h1 id="💻-작성-코드-리팩터링-전">💻 작성 코드 (리팩터링 전)</h1>
<pre><code class="language-python">import sys

def check_palindrome(input_str):
    start_idx = 0
    end_idx = len(input_str) - 1
    is_pseudo_palindrome = False
    while start_idx &lt; end_idx:
        if input_str[start_idx] == input_str[end_idx]:
            start_idx += 1
            end_idx -= 1
            continue

        if is_pseudo_palindrome:
            return 2

        if input_str[start_idx + 1] == input_str[end_idx] and input_str[start_idx] == input_str[end_idx - 1]:
            tmp_start = start_idx + 1
            tmp_end = end_idx
            is_tmp_pseudo_palindrome = False
            while tmp_start &lt; tmp_end:
                if input_str[tmp_start] == input_str[tmp_end]:
                    tmp_start += 1
                    tmp_end -= 1
                    continue

                is_tmp_pseudo_palindrome = True
                break

            if not is_tmp_pseudo_palindrome:
                return 1

            tmp_start = start_idx
            tmp_end = end_idx - 1
            is_tmp_pseudo_palindrome = False
            while tmp_start &lt; tmp_end:
                if input_str[tmp_start] == input_str[tmp_end]:
                    tmp_start += 1
                    tmp_end -= 1
                    continue

                is_tmp_pseudo_palindrome = True
                break

            if not is_tmp_pseudo_palindrome:
                return 1

            return 2

        if input_str[start_idx + 1] == input_str[end_idx]:
            start_idx += 1
            is_pseudo_palindrome = True
            continue

        if input_str[start_idx] == input_str[end_idx - 1]:
            is_pseudo_palindrome = True
            end_idx -= 1
            continue

        return 2

    if is_pseudo_palindrome:
        return 1

    return 0

readline = sys.stdin.readline
T = int(readline())
input_strs = []
for i in range(T):
    input_strs.append(readline().rstrip('\n'))

for input_str in input_strs:
    print(check_palindrome(input_str))</code></pre>
<br />

<hr />
<br />

<h1 id="🎯-접근-방식">🎯 접근 방식</h1>
<ol>
<li>문자열이 대칭인지 확인하기 위해 문자열의 양쪽 끝에 투포인터를 두고 중앙으로 이동시킨다.</li>
<li>각 포인터가 위치한 문자가 같은지 아닌지 비교하여 포인터를 이동한다.
 2-1. 대칭인 경우 포인터를 하나씩 이동시킨다.
 2-2. 대칭이 아니고 이미 문자를 제거했던 경우(<code>is_pseudo_palindrome == True</code>), 2를 반환한다.
 2-3. 대칭이 아닌 경우 이전에 문자를 제거하지 않았던 경우<ul>
<li>2-3-1. 왼쪽과 오른쪽 중에 한쪽 문자만 제거할 수 있는 경우, 문자를 제거하도록 포인터를 이동한 후 <code>is_pseudo_palindrome</code>의 값을 <code>True</code>로 변경한다.</li>
<li>2-3-2. 왼쪽 문자를 제거해도 되고, 오른쪽 문자를 제거해도 되는 경우는 둘 중에 하나만 최종적으로 대칭이 성립해도 유사회문이 된다. 먼저 왼쪽 문자를 제거하고 반복문을 통해 최종적으로 대칭이 되는지 확인해 만약 대칭이라면 1을 반환한다. 왼쪽 문자를 제거한 경우 최종적으로 대칭이 되지 않는다면, 오른쪽 문자를 제거하고 반복문을 통해 최종적으로 대칭이 되는지 확인한다. 만약 대칭이라면 1을 반환하고, 아니라면 2를 반환한다.</li>
</ul>
</li>
</ol>
<br />

<hr />
<br />

<h1 id="💡-개선사항">💡 개선사항</h1>
<ol>
<li>문자 제거가 일어나는 경우, 제거한 후에 최종적으로 대칭이 되는지 확인해야 하기 때문에 한쪽 문자만 제거할 수 있는 경우를 굳이 분리할 필요가 없다.</li>
<li>왼쪽 또는 오른쪽 문자를 제거한 후 최종적으로 대칭이 되는지 확인하는 while문은 별도의 메서드로 분리할 수 있다.</li>
<li>처음에 설계한 코드가 제출하면 틀려서, 반례를 찾는데 시간을 많이 소요했다. (e.g. <code>ababbabaa</code> 같은 케이스) 처음부터 설계 과정에서 여러 케이스를 떠올리며 로직을 설계하는 연습을 해야겠다. </li>
</ol>
<br />

<hr />
<br />


<h1 id="💻-최종-코드-리팩터링-후">💻 최종 코드 (리팩터링 후)</h1>
<pre><code class="language-python">import sys

def is_palindrome(s, left, right):
    while left &lt; right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    return True

def check_palindrome_or_not(input_str):
    start_idx = 0
    end_idx = len(input_str) - 1

    while start_idx &lt; end_idx:
        if input_str[start_idx] == input_str[end_idx]:
            start_idx += 1
            end_idx -= 1
            continue

        # 두 경우 중에 하나라도 회문이면 유사 회문
        if is_palindrome(input_str, start_idx + 1, end_idx) or is_palindrome(input_str, start_idx, end_idx - 1):
            return 1
        return 2

    return 0

readline = sys.stdin.readline
T = int(readline())
input_strs = []
for i in range(T):
    input_strs.append(readline().rstrip('\n'))

for input_str in input_strs:
    print(check_palindrome_or_not(input_str))</code></pre>
<br />

<hr />
<br />

<p>[ktb-algorithm-study] 1주차</p>