<h1 id="📌-문제-정보">📌 문제 정보</h1>
<p>링크: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/17681">https://school.programmers.co.kr/learn/courses/30/lessons/17681</a></p>
<p>유형: <code>구현</code>, <code>비트마스크</code></p>
<p>난이도: <code>Lv.1</code></p>
<p>스스로 풀었는가? ✅</p>
<p>특이사항: 2018 KAKAO BLIND RECRUITMENT 문제</p>
<br />

<hr />
<br />


<h1 id="💻-작성-코드">💻 작성 코드</h1>
<pre><code class="language-python">def solution(n, arr1, arr2):
    answer = []
    SPACE = &quot; &quot;
    WALL = &quot;#&quot;
    for row_idx in range(n):
        decoded_row_arr1 = list(bin(arr1[row_idx])[2:])
        decoded_row_arr2 = list(bin(arr2[row_idx])[2:])
        if len(decoded_row_arr1) &lt; n:
            len_diff = n - len(decoded_row_arr1)
            decoded_row_arr1 = [0] * len_diff + decoded_row_arr1

        if len(decoded_row_arr2) &lt; n:
            len_diff = n - len(decoded_row_arr2)
            decoded_row_arr2 = [0] * len_diff + decoded_row_arr2

        row = []
        for col_idx in range(n):
            if decoded_row_arr1[col_idx] == &quot;1&quot; or decoded_row_arr2[col_idx] == &quot;1&quot;:
                row.append(WALL)
                continue

            row.append(SPACE)
        answer.append(''.join(row))
    return answer</code></pre>
<br />


<hr />
<br />

<h1 id="🎯-접근-방식">🎯 접근 방식</h1>
<ol>
<li>정수 배열의 row를 하나씩 읽어 바이너리로 변환 후, 리스트로 변환한다.</li>
<li>리스트의 길이가 <code>n</code>보다 작은 경우 부족한 길이만큼 왼쪽에 <code>0</code>을 붙인다. (n=5일 때 <code>'1001'</code> -&gt; <code>'01001'</code>)</li>
<li>두 지도의 배열 중 하나라도 <code>1</code>인 경우 <code>벽(#)</code>을 넣고, 아니라면 <code>공백(&quot; &quot;)</code>을 넣는다.</li>
<li>해독된 <code>row</code>를 리스트에서 문자열로 변환해 정답 배열에 넣는다.</li>
</ol>
<br />

<hr />
<br />

<h1 id="💡-개선사항">💡 개선사항</h1>
<p>프로그래머스에서 다른 사람의 풀이를 구경하다가 천재적인 코드를 발견했다.</p>
<pre><code class="language-python">def solution(n, arr1, arr2):
    answer = []
    for i,j in zip(arr1,arr2):
        a12 = str(bin(i|j)[2:])
        a12=a12.rjust(n,'0')
        a12=a12.replace('1','#')
        a12=a12.replace('0',' ')
        answer.append(a12)
    return answer</code></pre>
<ol>
<li><p><code>row_idx</code>, <code>col_idx</code>처럼 인덱스로 접근하는 대신 .zip()를 이용하면 두 배열의 값을 한번에 읽을 수 있다.</p>
</li>
<li><p>문자열의 길이를 맞추는 것은 rjust, zfill을 이용하면 된다.</p>
<pre><code class="language-python"># 문자열의 길이를 5로 맞추고 왼쪽을 '0'으로 채움
result = original.zfill(5)

# 문자열의 길이를 5로 맞추고 왼쪽을 '0'으로 채움
result2 = original.rjust(5, '0')</code></pre>
<p>zfill은 항상 0으로 채우는 반면, rjust는 문자를 지정할 수 있다는 차이가 있다. 내 코드에 적용하면 <code>bin(number)[2:].zill(n)</code> 이 되겠다.</p>
</li>
<li><p>리스트 컴프리헨션을 이용하면 코드를 더욱 간결하게 만들 수 있다.</p>
</li>
<li><p>문자열의 각 문자에 대한 순회를 위해 리스트를 만들 필요가 없다. for...in 문을 통해 간편하게 문자열의 각 문자를 순회할 수 있다.</p>
</li>
<li><p>비트 OR 연산을 이용하면 두 지도의 하나라도 벽이 있는지 간단하게 확인할 수 있다.</p>
<pre><code class="language-python">row1 = 9    # 이진수: 1001
row2 = 30   # 이진수: 11110
</code></pre>
</li>
</ol>
<p>&quot;&quot;&quot;
row1 | row2 연산</p>
<p>  01001   # 9의 이진수 (앞에 0을 붙여 5비트로 맞춤)
  11110   # 30의 이진수</p>
<hr />
<p>  11111   # OR 연산 결과</p>
<p>따라서 row1 | row2는 32를 의미한다.
&quot;&quot;&quot;
print(row1 | row2) # 32
print(bin(row1 | row2)) # '0b11111'</p>
<pre><code>

&lt;br /&gt;

---

&lt;br /&gt;

# 💻 개선사항을 반영한 최종 코드


```python
def solution(n, arr1, arr2):
    answer = []
    SPACE = &quot; &quot;
    WALL = &quot;#&quot;

    for row1, row2 in zip(arr1, arr2):
        # 비트 OR 연산 후 이진수 문자열로 변환
        combined_row = bin(row1 | row2)[2:].rjust(n, '0')

        # 리스트 컴프리헨션을 사용하여 정답 지도의 row 생성
        decoded_row = [WALL if bit == &quot;1&quot; else SPACE for bit in combined_row]

        answer.append(''.join(decoded_row))

    return answer</code></pre><br />

<hr />
<br />

<p>[ktb-algorithm-study] 1주차</p>