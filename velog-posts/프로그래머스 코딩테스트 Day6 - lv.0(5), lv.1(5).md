<h2 id="🔎-주요-문제-풀이">🔎 주요 문제 풀이</h2>
<h3 id="옷가게-할인-받기">옷가게 할인 받기</h3>
<blockquote>
<p>머쓱이네 옷가게는 10만 원 이상 사면 5%, 30만 원 이상 사면 10%, 50만 원 이상 사면 20%를 할인해줍니다.
구매한 옷의 가격 price가 주어질 때, 지불해야 할 금액을 return 하도록 solution 함수를 완성해보세요.</p>
</blockquote>
<h4 id="🔷-풀이">🔷 풀이</h4>
<pre><code class="language-js">function solution(price) {
    const result = price &gt;= 500000 ? price * 0.8
    : price &gt;= 300000 ? price * 0.9
    : price &gt;= 100000 ? price * 0.95
    : price

    return parseInt(result)
}</code></pre>
<ul>
<li>조건 순서 잘 생각하기</li>
</ul>
<h4 id="🔶-다른-사람의-풀이">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">const discounts = [
    [500000, 20],
    [300000, 10],
    [100000, 5],
]

function solution(price) {
    for(const discount of discounts)
        if(price &gt;= discount[0])
            return Math.floor(price * (1 - discount[1] / 100))
    return price
}</code></pre>
<ul>
<li><code>discounts</code> 배열을 정의함으로써 코드 흐름이 더욱 명확해진 것 같다.</li>
<li><code>for</code>문과 <code>if</code>문이 각각 한 줄이기 때문에 <code>{}</code> 생략</li>
</ul>
<hr />
<h3 id="자릿수-더하기">자릿수 더하기</h3>
<blockquote>
<p>자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수를 만들어 주세요.
예를들어 N = 123이면 1 + 2 + 3 = 6을 return 하면 됩니다.</p>
</blockquote>
<h4 id="🔷-풀이-1">🔷 풀이</h4>
<pre><code class="language-js">function solution(n) {
    const arr = String(n).split('')
    let sum = 0

    for(let i = 0; i &lt; arr.length; i++) {
        sum += Number(arr[i])
    }

    return sum
}</code></pre>
<h4 id="🔶-다른-사람의-풀이-1">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">function solution(n) {
    return String(n)
        .split('')
        .reduce((acc, cur) =&gt; acc + Number(cur), 0)
}</code></pre>
<ul>
<li><code>reduce()</code> 활용</li>
</ul>
<hr />
<h2 id="📝-필요-내용-정리">📝 필요 내용 정리</h2>
<h3 id="mapcallback">map(callback)</h3>
<p>배열의 각 요소를 <code>callback</code> 함수에 넣어서 반환한 결과로 새 배열을 만듦</p>
<pre><code class="language-js">[&quot;1&quot;, &quot;2&quot;, &quot;3&quot;].map(Number) // [1, 2, 3]</code></pre>
<h4 id="--예외">- 예외</h4>
<pre><code class="language-js">[&quot;1&quot;, &quot;2&quot;, &quot;3&quot;].map(parseInt) // [1, NaN, NaN]</code></pre>
<p><strong>- 원인: <code>parseInt(x, index)</code>처럼 두 번째 인자를 해석해서 생기는 문제</strong></p>
<ul>
<li><code>map</code>은 내부적으로 2개의 인자를 콜백 함수에 넘김<ul>
<li><code>arr.map((value, index) =&gt; ...)</code><ul>
<li>1번째 인자: 현재 요소 (<code>value</code>)</li>
<li>2번째 인자: 현재 인덱스 (<code>index</code>)</li>
</ul>
</li>
</ul>
</li>
<li><code>parseInt</code> 함수의 형태<ul>
<li><code>parseInt(string, radix)</code><ul>
<li>1번째 인자: 문자열을 숫자로 바꿀 대상 (<code>string</code>)</li>
<li>2번째 인자: 몇 진수로 바꿀지 (<code>radix</code>)</li>
</ul>
</li>
</ul>
</li>
</ul>
<p><strong>- 결과적으로 호출되는 형태는 아래와 같음</strong></p>
<pre><code class="language-js">parseInt(&quot;1&quot;, 0)  // → 1 (radix 0은 자동 감지 → 10진수)
parseInt(&quot;2&quot;, 1)  // → NaN (1진법은 없음 → 잘못된 radix)
parseInt(&quot;3&quot;, 2)  // → NaN (&quot;3&quot;은 2진법에서 유효하지 않음)

// 결과: [1, NaN, NaN]</code></pre>
<p><strong>- 해결방법</strong></p>
<ul>
<li>명시적으로 10진수 설정하기<pre><code class="language-js">[&quot;1&quot;, &quot;2&quot;, &quot;3&quot;].map(x =&gt; parseInt(x, 10)) // → [1, 2, 3]</code></pre>
</li>
</ul>
<hr />
<h3 id="reverse">reverse()</h3>
<p><strong>배열</strong>의 순서를 반대로 바꿈</p>
<ul>
<li>원본 배열을 직접 변경</li>
<li>새로운 배열을 반환하는 게 아니라 <strong>바뀐 자기 자신을 반환</strong><pre><code class="language-js">const arr = [1, 2, 3, 4, 5];
const reversed = arr.reverse();
</code></pre>
</li>
</ul>
<p>console.log(reversed); // [5, 4, 3, 2, 1]
console.log(arr);      // [5, 4, 3, 2, 1] ← 원본도 바뀜!</p>
<p>```</p>
<hr />
<h2 id="🗂️-문제-목록-10개">🗂️ 문제 목록 (10개)</h2>
<h4 id="lv0-5개">lv.0 (5개)</h4>
<p>중복된 숫자 개수
배열 두 배 만들기
중앙값 구하기
짝수는 싫어요
옷가게 할인 받기🏷️</p>
<h4 id="lv1-5개">lv.1 (5개)</h4>
<p>약수의 합
자릿수 더하기🏷️
자연수 뒤집어 배열로 만들기
짝수와 홀수
평균 구하기</p>