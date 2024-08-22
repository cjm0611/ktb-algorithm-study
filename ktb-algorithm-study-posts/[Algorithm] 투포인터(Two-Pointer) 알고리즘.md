<h1 id="투-포인터two-pointer란">투 포인터(Two Pointer)란?</h1>
<p><code>2개의 포인터</code>를 사용하여 특정 조건을 만족하는 구간이나 숫자의 쌍을 구하는 알고리즘이다. 주로 <code>정렬된 배열</code>에서 사용된다. 정렬되지 않은 배열이라면 <code>누적합</code>을 이용해 정렬된 배열의 형태로 바꿔 사용할 수 있다.</p>
<br />

<h2 id="동작-방식">동작 방식</h2>
<p>다음과 같이 정렬된 배열을 생각해보자.
<img alt="" src="https://velog.velcdn.com/images/cjm-0611/post/034227e0-8e70-4098-b56e-586a37ec098e/image.png" /></p>
<p><code>left</code>는 탐색 범위의 <code>시작</code>을 나타내는 왼쪽 포인터이다.
<code>right</code>는 탐색 범위의 <code>끝</code>을 나타내는 오른쪽 포인터이다.
우리가 선택한 구간은 <code>left ~ right</code>이 된다.</p>
<br />

<p><img alt="" src="https://velog.velcdn.com/images/cjm-0611/post/033f7003-9b93-4854-ac5c-b54b41ea829c/image.png" />right 포인터가 3에 위치한다면, 구간은 <code>1~3</code>이 되며 그때의 <code>sum</code>은 <code>1+2+3</code>이 된다.</p>
<br />

<p>만약 문제에서 <code>목표 값 N</code>이 주어진다면, sum과 N을 비교하여 포인터만 움직이면 된다.</p>
<blockquote>
<p><strong>투 포인터 이동 원칙</strong></p>
</blockquote>
<ul>
<li>sum &gt; N: left를 오른쪽으로 이동한다. sum의 값은 작아진다.</li>
<li>sum &lt; N: right를 오른쪽으로 이동한다. sum의 값은 커진다.</li>
<li>sum == N: 정답을 찾았다. 계속 탐색하려면 right를 오른쪽으로 이동한다. sum의 값은 커진다.</li>
</ul>
<p>현재 상태 <code>sum</code>과 목표 <code>N</code>을 비교하면서 목표에 가까워지도록 포인터를 이동한다. 특정 조건을 만족하는 범위를 찾거나, 특정 조건을 만족하는 수의 쌍을 찾는데 유용하다.</p>
<br />


<h2 id="시간-복잡도">시간 복잡도</h2>
<p>투 포인터 알고리즘의 시간 복잡도는 일반적으로 <strong>O(n)</strong>이다. 그 이유는 두 개의 포인터가 배열의 시작과 끝에서 출발하여 각 포인터가 배열을 최대 한 번만 순회하기 때문이다.</p>
<br />

<hr />
<br />

<h1 id="예제-백준-2018번-수들의-합5">(예제) 백준 2018번 "수들의 합5"</h1>
<h2 id="문제-정보">문제 정보</h2>
<ul>
<li>링크: <a href="https://www.acmicpc.net/problem/2018">https://www.acmicpc.net/problem/2018</a></li>
<li>난이도: <code>실버 5</code></li>
</ul>
<br />

<h2 id="문제-요약">문제 요약</h2>
<p>입력으로 정수 N이 주어진다. N을 몇 개의 연속된 자연수의 합으로 나타내는 가지수를 구해라. 이때, 사용하는 자연수는 N이하여야 한다.</p>
<p>예시1. 입력으로 15가 주어짐
15를 나타내는 방법은 <code>15</code>, <code>7+8</code>, <code>4+5+6</code>, <code>1+2+3+4+5</code>의 4가지가 있다. =&gt; 정답 4</p>
<p>예시2. 입력으로 10이 주어짐
10을 나타내는 방법은 <code>10</code>, <code>1+2+3+4</code>의 2가지가 있다. =&gt; 정답 2</p>
<br />

<h2 id="문제-풀이">문제 풀이</h2>
<p>1부터 15까지 자연수가 나열되어있다고 생각해보자. 우리의 목표는 15를 연속된 자연수의 합으로 나타내는 것이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/cjm-0611/post/9f6e3dcd-037b-478b-9878-9ed020209f88/image.png" /></p>
<p>left = 1, right = 1
left부터 right까지의 합은 1이다.
목표인 15보다 작으므로 right를 이동한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/cjm-0611/post/fa9437e1-6bd9-4414-807b-176109efc852/image.png" /></p>
<p>left = 1, right = 2
left부터 right까지의 합은 1+2 = 3이다.
목표인 15보다 작으므로 right를 이동한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/cjm-0611/post/2a781702-b7da-4749-b542-cf292ea1640b/image.png" /></p>
<p>left = 1, right = 3
left부터 right까지의 합은 1+2+3 = 6이다.
목표인 15보다 작으므로 right를 이동한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/cjm-0611/post/6b4c4e71-6bbb-4a0b-a679-a07314666b27/image.png" /></p>
<p>left = 1, right = 4
left부터 right까지의 합은 1+2+3+4 = 10이다.
목표인 15보다 작으므로 right를 이동한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/cjm-0611/post/84368064-08cf-4651-81a3-738b37790494/image.png" /></p>
<p>left = 1, right = 5
left부터 right까지의 합은 <strong>1+2+3+4+5 = 15</strong>이다.
<strong>목표값과 동일하므로, 정답의 개수를 +1 시킨다. (누적: 1개)</strong>
<strong>그리고 right를 이동한다.</strong></p>
<p><img alt="" src="https://velog.velcdn.com/images/cjm-0611/post/46dc038e-f1a8-4bcc-9a30-e5c396cb3983/image.png" /></p>
<p>left = 1, right = 6
left부터 right까지의 합은 1+2+3+4+5+6 = 21이다.
목표인 15보다 크므로 left를 이동한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/cjm-0611/post/3d90d39c-d8fa-455b-b271-591a67386e7f/image.png" /></p>
<p>left = 2, right = 6
left부터 right까지의 합은 2+3+4+5+6 = 20이다.
목표인 15보다 크므로 left를 이동한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/cjm-0611/post/f28eb49b-6368-46f8-b13c-016bafa7130d/image.png" /></p>
<p>left = 3, right = 6
left부터 right까지의 합은 3+4+5+6 = 18이다.
목표인 15보다 크므로 left를 이동한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/cjm-0611/post/549dfb5b-91d9-434e-9acf-26b713d30553/image.png" /></p>
<p>left = 4, right = 6
left부터 right까지의 합은 <strong>4+5+6 = 15</strong>이다.
<strong>목표값과 동일하므로, 정답의 개수를 +1 시킨다. (누적: 2개)</strong>
<strong>그리고 right를 이동한다.</strong></p>
<p>.
.
.</p>
<p>(반복)</p>
<p>그 다음은 어떻게 될까?
right를 이동하면 목표값보다 커지므로 다시 left를 이동할 것이다. 이 과정을 반복하면 두 포인터가 계속 오른쪽으로 움직이게 되며, 다른 정답인 <code>7+8(left=7, right=8)</code>, <code>15(left=15, right=15)</code>을 찾아 정답이 4개가 된다.</p>
<br />

<hr />
<br />

<h2 id="풀이-코드">풀이 코드</h2>
<pre><code class="language-python">import sys

realine = sys.stdin.readline
N = int(realine())

left = 1 # 왼쪽 포인터
right = 1 # 오른쪽 포인터
sum = 1 # 현재까지의 합
answer_count = 0

while right &lt;= N: # right가 오른쪽 끝에 도달할 때까지 진행
    if sum &gt; N:
        sum -= left
        left += 1
    elif sum &lt; N:
        right += 1
        sum += right
    else: # sum == N
        answer_count += 1
        right += 1
        sum += right

print(answer_count)</code></pre>
<p>위에서 적었던 투포인터의 이동 법칙을 상기시켜보자.</p>
<blockquote>
<p><strong>투 포인터 이동 원칙</strong>
sum &gt; N: left를 오른쪽으로 이동한다. sum의 값은 작아진다.
sum &lt; N: right를 오른쪽으로 이동한다. sum의 값은 커진다.
sum == N: 정답을 찾았다. 계속 탐색하려면 right를 오른쪽으로 이동한다. sum의 값은 커진다.</p>
</blockquote>
<h3 id="1번-케이스-sum--n">1번 케이스) <code>sum &gt; N</code></h3>
<pre><code class="language-python">    if sum &gt; N:
        sum -= left
        left += 1</code></pre>
<p>sum이 N보다 큰 경우를 생각해보자.
<img alt="" src="https://velog.velcdn.com/images/cjm-0611/post/e52b0727-3c9b-43ef-be74-027340521ab7/image.png" />
left=1, right=6일 때, sum = 1+2+3+4+5+6 = 21이다.
목표한 값보다 크므로 left를 오른쪽으로 이동하고, sum에서 1을 빼고 싶다.
sum에서 1을 빼기 위해서는 sum에서 left를 먼저 뺀 후(sum -= 1), left를 이동시켜야 한다.(left=2)</p>
<br />

<h3 id="2번-케이스-sum--n">2번 케이스) <code>sum &lt; N</code></h3>
<pre><code class="language-python">    elif sum &lt; N:
        right += 1
        sum += right</code></pre>
<p>sum이 N보다 작은! 경우를 생각해보자.
<img alt="" src="https://velog.velcdn.com/images/cjm-0611/post/98ba59f7-c0da-493a-82cb-f1292565f528/image.png" /></p>
<p>left=1, right=3일 때, sum = 1+2+3 = 6이다.
목표한 값보다 작으므로 right를 오른쪽으로 이동하고, sum에 4를 더하고 싶다.
sum에 4를 더하기 위해서는 right를 4로 먼저 이동시킨 후(right=4), sum에 더해야 한다.(sum += 4)</p>
<br />

<h3 id="3번-케이스-sum--n">3번 케이스) <code>sum == N</code></h3>
<pre><code class="language-python">    else: # sum == N
        answer_count += 1
        right += 1
        sum += right</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/cjm-0611/post/17ac79b7-726d-4051-b1b3-3064a48bd13e/image.png" /></p>
<p>left=4, right=6일 때, sum = 4+5+6 = 15이다.
목표한 값과 동일하므로 정답 개수를 1 늘린다.
정답이 1개였다면 반복문을 종료했겠지만, N을 만드는 연속된 자연수의 합은 여러 개일수 있으므로 탐색을 계속한다.
right를 7로 이동시킨 뒤, sum에 right를 더한다.
(그러면 sum이 N보다 커지므로 그 다음엔 left가 이동하고, 위의 과정이 반복될 것이다.)</p>
<br />

<hr />
<br />

<h1 id="정리">정리</h1>
<h2 id="투-포인터는-언제-쓰는가">투 포인터는 언제 쓰는가?</h2>
<p>정렬된 배열에서의 특정 조건을 만족하는 요소 쌍이나 부분 배열을 찾는 데 자주 사용된다. 정렬된 배열의 특성을 이용하여 두 포인터를 배열의 왼쪽에서 시작하거나 양 끝에서 시작함으로써 문제를 해결할 수 있다.</p>
<blockquote>
<p>투 포인터가 양쪽 끝에서 시작하는 경우?
left는 배열의 가장 왼쪽에, right는 배열에 가장 오른쪽에 위치시켜 합이 목표 값보다 작으면 왼쪽 포인터를 오른쪽으로 이동시키고, 크면 오른쪽 포인터를 왼쪽으로 이동시키는 방법</p>
</blockquote>
<br />

<h3 id="누적합과의-조합">누적합과의 조합</h3>
<p>투 포인터 알고리즘은 <strong>누적합(prefix sum)</strong>과 함께 쓰이기도 한다.
<strong>위의 예제처럼 풀기 위해서는 배열이 정렬되어있어야 한다.</strong>
마구잡이인 배열에서 특정 합을 갖는 부분 배열을 구해야 한다면 누적합을 이용할 수 있다.
각 인덱스까지의 합을 미리 구해 놓고, 두 포인터를 사용하여 누적합의 차이가 특정 값을 만족하는 부분 배열을 찾으면 된다.</p>
<br />

<hr />
<br />

<h1 id="슬라이딩-윈도우와의-차이점">슬라이딩 윈도우와의 차이점</h1>
<p>슬라이딩 윈도우는 고정 길이를 갖는다. 예를 들어 가로 길이가 5라고 고정되어 있어서 한쪽의 포인터가 움직이면 다른쪽의 포인터도 움직인다.
가변 길이의 슬라이딩 윈도우가 투포인터라고 생각하면 될 것 같다.</p>
<br />

<hr />
<br />

<h1 id="참고자료">참고자료</h1>
<p>&lt;Do it! 알고리즘 코딩 테스트 - 자바 편&gt;</p>
<br />

<hr />
<p>[ktb-algorithm-study] 2주차</p>