<h2 id="🔎-주요-문제-풀이">🔎 주요 문제 풀이</h2>
<h3 id="원소들의-곱과-합">원소들의 곱과 합</h3>
<blockquote>
<p>정수가 담긴 리스트 num_list가 주어질 때, 모든 원소들의 곱이 모든 원소들의 합의 제곱보다 작으면 1을 크면 0을 return하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이">🔷 풀이</h4>
<p><strong>- <code>reduce</code> 메서드 활용</strong></p>
<pre><code class="language-js">function solution(num_list) {
    const sum = num_list.reduce((a, b) =&gt; a + b, 0)
    const multipled = num_list.reduce((a, b) =&gt; a * b, 1)

    return multipled &lt; sum ** 2 ? 1 : 0
}</code></pre>
<ul>
<li>곱셈의 초기값은 1로 세팅 주의</li>
</ul>
<p><strong>- <code>for</code>문 활용</strong></p>
<pre><code class="language-js">function solution(num_list) {
    let sum = 0;
    let multipled = 1;

    for(let i = 0; i &lt; num_list.length; i++) {
        sum += num_list[i];
        multipled *= num_list[i];
    }

    return multipled &lt; sum ** 2 ? 1 : 0;
}</code></pre>
<h4 id="🔶-다른-사람의-풀이">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">function solution(num_list) {
    let sum = 0;
    let multipled = 1;

    for(const num of num_list) {
        sum += num
        multipled *= num
    }

    return multipled &lt; sum ** 2 ? 1 : 0;
}</code></pre>
<ul>
<li><code>for...of</code>문 활용으로 조건을 더 간단하게 작성 가능</li>
</ul>
<hr />
<h3 id="문자-반복-출력하기">문자 반복 출력하기</h3>
<blockquote>
<p>문자열 my_string과 정수 n이 매개변수로 주어질 때, my_string에 들어있는 각 문자를 n만큼 반복한 문자열을 return 하도록 solution 함수를 완성해보세요.</p>
</blockquote>
<h4 id="🔷-풀이-1">🔷 풀이</h4>
<pre><code class="language-js">function solution(my_string, n) {
    return my_string
        .split('')
        .map((x) =&gt; x.repeat(n))
        .join('')
}</code></pre>
<ul>
<li><code>map()</code>과 <code>repeat()</code>이 떠오르지 않았다..</li>
</ul>
<h4 id="🔶-다른-사람의-풀이-1">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">function solution(my_string, n) {
    return [...my_string]
        .map((x) =&gt; x.repeat(n))
        .join('')
}</code></pre>
<ul>
<li><code>split()</code> 대신 <code>spread</code> 문법을 활용</li>
</ul>
<hr />
<h3 id="이어-붙인-수">이어 붙인 수</h3>
<blockquote>
<p>정수가 담긴 리스트 num_list가 주어집니다. num_list의 홀수만 순서대로 이어 붙인 수와 짝수만 순서대로 이어 붙인 수의 합을 return하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이-2">🔷 풀이</h4>
<pre><code class="language-js">function solution(num_list) {
    let odd = '';
    let even = '';

    for (let i = 0; i &lt; num_list.length; i++) {
        num_list[i] % 2 === 0
        ? even += String(num_list[i])
        : odd += String(num_list[i])
    }

    return  Number(odd) + Number(even)
}</code></pre>
<ul>
<li><strong>암묵적 형변환</strong><ul>
<li><code>even</code>은 문자열(<code>''</code>)로 초기화되어 있음</li>
<li><code>num_list[i]</code>는 숫자</li>
<li><code>문자열 += 숫자</code> 형태가 되면 숫자가 자동으로 문자열로 바뀜</li>
<li><em>-&gt; <code>String()</code> 변환 불필요*</em></li>
</ul>
</li>
</ul>
<h4 id="🔶-다른-사람의-풀이-2">🔶 다른 사람의 풀이</h4>
<p><strong>- <code>reduce()</code> 활용</strong></p>
<pre><code class="language-js">function solution(num_list) {
    const {odds, evens} = num_list.reduce(({odds, evens}, num) =&gt; {
        if (num % 2 === 0) {
            evens.push(num)
        } else {
            odds.push(num)
        }
        return { odds, evens }
    }, {odds: [], evens: []})

    return Number(odds.join('')) + Number(evens.join(''))
}</code></pre>
<ul>
<li><code>reduce()</code> 구조<ul>
<li>누적값을 반드시 <code>return</code> 해야 함!</li>
<li><code>initialValue</code>: 초기 누적값<pre><code class="language-js">array.reduce((accumulator, currentValue) =&gt; {
// 로직
return accumulator;
}, initialValue);</code></pre>
</li>
</ul>
</li>
</ul>
<hr />
<h2 id="📝-필요-내용-정리">📝 필요 내용 정리</h2>
<h3 id="for문-정리"><code>for</code>문 정리</h3>
<ul>
<li><p><code>for...of</code></p>
<ul>
<li>배열, 문자열, Map, Set 등 이터러블(iterable)한 값(value) 순회</li>
</ul>
</li>
<li><p><code>for...in</code></p>
<ul>
<li>객체(object)의 속성명(key) 순회</li>
</ul>
</li>
<li><p><code>for (let i = ...)</code></p>
<ul>
<li>배열의 인덱스를 수동으로 제어하여, 인덱스 및 조건문 활용 가능</li>
</ul>
</li>
</ul>
<pre><code class="language-js">    const obj = { a: 1, b: 2 };

    for (const key in obj) {
      console.log(key);       // 'a', 'b'
      console.log(obj[key]);  // 1, 2
}</code></pre>
<h3 id="slice-n">slice(-n)</h3>
<ul>
<li>음수 인덱스를 활용하여, 뒤에서부터 자르기<pre><code class="language-js">&quot;Programmer123&quot;.slice(-3); // &quot;123&quot;</code></pre>
</li>
</ul>
<hr />
<h2 id="🗂️-문제-목록-5개">🗂️ 문제 목록 (5개)</h2>
<p>n 번째 원소까지
원소들의 곱과 합🏷️
문자열의 뒤의 n글자
문자 반복 출력하기🏷️
이어 붙인 수🏷️</p>