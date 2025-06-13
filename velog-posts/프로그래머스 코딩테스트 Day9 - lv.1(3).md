<h2 id="🔎-주요-문제-풀이">🔎 주요 문제 풀이</h2>
<h3 id="나누어-떨어지는-숫자-배열">나누어 떨어지는 숫자 배열</h3>
<blockquote>
<p>array의 각 element 중 divisor로 나누어 떨어지는 값을 오름차순으로 정렬한 배열을 반환하는 함수, solution을 작성해주세요.
divisor로 나누어 떨어지는 element가 하나도 없다면 배열에 -1을 담아 반환하세요.</p>
</blockquote>
<h4 id="🔷-풀이">🔷 풀이</h4>
<p><strong>- 1번째 풀이</strong></p>
<pre><code class="language-js">function solution(arr, divisor) {
    const num_list = arr.sort((a, b) =&gt; a - b)
    let answer = []

    for(let i = 0; i &lt; num_list.length; i++) {
        if(num_list[i] % divisor === 0) {
            answer.push(num_list[i])
        }
    }

    if (!answer.length) answer = [-1]

    return answer
}</code></pre>
<ul>
<li><strong>명령형, 수학적 연산 중심 로직</strong></li>
<li>빈 배열인지 확인할 때 <code>length</code>로 확인하도록 주의</li>
<li><code>return</code>문 잊지말고 잘 쓰자</li>
</ul>
<p><strong>- 2번째 풀이</strong></p>
<pre><code class="language-js">function solution(arr, divisor) {
    const num_list = arr.filter((x) =&gt; x % divisor === 0).sort((a, b) =&gt; a - b)

    return num_list.length ? num_list : [-1]
}</code></pre>
<ul>
<li><strong>선언형, 함수형 기반 로직</strong></li>
</ul>
<hr />
<h3 id="콜라츠-추측">콜라츠 추측</h3>
<blockquote>
<p>1937년 Collatz란 사람에 의해 제기된 이 추측은, 주어진 수가 1이 될 때까지 다음 작업을 반복하면, 모든 수를 1로 만들 수 있다는 추측입니다. 작업은 다음과 같습니다.
<strong>1-1. 입력된 수가 짝수라면 2로 나눕니다. 
1-2. 입력된 수가 홀수라면 3을 곱하고 1을 더합니다.
2. 결과로 나온 수에 같은 작업을 1이 될 때까지 반복합니다.</strong> 
예를 들어, 주어진 수가 6이라면 6 → 3 → 10 → 5 → 16 → 8 → 4 → 2 → 1 이 되어 총 8번 만에 1이 됩니다. 위 작업을 몇 번이나 반복해야 하는지 반환하는 함수, solution을 완성해 주세요. 단, 주어진 수가 1인 경우에는 0을, 작업을 500번 반복할 때까지 1이 되지 않는다면 –1을 반환해 주세요.</p>
</blockquote>
<h4 id="🔷-풀이-1">🔷 풀이</h4>
<p><strong>- 1번째 풀이</strong></p>
<pre><code class="language-js">function solution(num) {
    let arr = []

    while(num !== 1) {
        if(arr.length &gt;= 500) return -1

        if(num % 2 === 0) {
            num = num / 2
        } else {
            num = num * 3 + 1
        }
        arr.push(num)
    }

    return arr.length
}</code></pre>
<p><strong>- 2번째 풀이</strong></p>
<pre><code class="language-js">function solution(num) {
    let count = 0

    while(num !== 1) {
        if(num % 2 === 0) {
            num = num / 2
        } else {
            num = num * 3 + 1
        }
        count ++

        if (count === 500) return -1
    }

    return count
}</code></pre>
<ul>
<li>굳이 배열을 만들 필요 없이, <code>count</code> 변수로 카운트 하기!
이런 류의 문제가 나왔을 때마다 놓치는 부분이다..🥲</li>
<li>이 경우는 삼항연산자보다 <code>if</code>문이 좀 더 가독성이 좋은 것 같음</li>
<li>좀 더 효율적으로 조건문을 처리하고 싶어서 고민을 많이 했는데, 우선 되는대로 작성부터 해놓고 리팩토링하는 방식으로 풀어나가는 것이 좋을 것 같다. 처음부터 어렵게 생각하지 말자.</li>
</ul>
<hr />
<h2 id="📝-필요-내용-정리">📝 필요 내용 정리</h2>
<h3 id="배열에서-특정-요소-찾기">배열에서 특정 요소 찾기</h3>
<h4 id="--indexof">- indexOf</h4>
<pre><code class="language-js">const arr = [1, 3, 5, 7, 9];

arr.indexOf(5); // 2
arr.indexOf(x =&gt; x &gt; 4);  // ❌ (조건식 넘기면 안 됨, 단순 값만 가능)</code></pre>
<ul>
<li>값만 넘겨서 찾음
: 단순 <code>===</code> 비교</li>
<li>문자열에서도 <code>indexOf</code> 메서드 존재<pre><code class="language-js">&quot;hello&quot;.indexOf(&quot;e&quot;);  // 1</code></pre>
</li>
</ul>
<h4 id="--findindex">- findIndex</h4>
<pre><code class="language-js">const arr = [1, 3, 5, 7, 9];

arr.findIndex(x =&gt; x &gt; 4); // 2 (5가 첫 번째로 조건을 만족)
arr.findIndex(x =&gt; x === 5); // 2 (indexOf처럼도 사용 가능)</code></pre>
<ul>
<li>조건식(함수)를 넘겨 검사함
: 콜백 함수의 <code>true/false</code> 여부로 판단</li>
</ul>
<h2 id="🗂️-문제-목록-3개">🗂️ 문제 목록 (3개)</h2>
<p>나누어 떨어지는 숫자 배열🏷️
서울에서 김서방 찾기
콜라츠 추측</p>