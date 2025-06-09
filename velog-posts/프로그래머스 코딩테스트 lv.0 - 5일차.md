<h2 id="🔎-주요-문제-풀이">🔎 주요 문제 풀이</h2>
<h3 id="n-번째-원소부터">n 번째 원소부터</h3>
<blockquote>
<p>정수 리스트 num_list와 정수 n이 주어질 때, n 번째 원소부터 마지막 원소까지의 모든 원소를 담은 리스트를 return하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이">🔷 풀이</h4>
<pre><code class="language-js">function solution(num_list, n) {
    return num_list.slice(n - 1, num_list.length)
}</code></pre>
<h4 id="🔶-다른-사람의-풀이">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">function solution(num_list, n) {
    return num_list.slice(n - 1)
}</code></pre>
<ul>
<li>3일차에서 정리했던 <code>slice()</code> 메서드 리마인드!<ul>
<li><code>slice(n)</code>: n번째 인덱스부터 반환</li>
<li><code>slice(start, end)</code>: <code>start</code>인덱스~<code>end - 1</code>인덱스 값 반환<pre><code class="language-js">&quot;abcdef&quot;.slice(0, 3); // &quot;abc&quot;
&quot;abcdef&quot;.slice(2); // &quot;cdef&quot;</code></pre>
</li>
</ul>
</li>
</ul>
<hr />
<h3 id="두-수의-연산값-비교하기">두 수의 연산값 비교하기</h3>
<blockquote>
<p>연산 ⊕는 두 정수에 대한 연산으로 두 정수를 붙여서 쓴 값을 반환합니다. 예를 들면 다음과 같습니다.
12 ⊕ 3 = 123
3 ⊕ 12 = 312
양의 정수 a와 b가 주어졌을 때, a ⊕ b와 2 * a * b 중 더 큰 값을 return하는 solution 함수를 완성해 주세요.
단, a ⊕ b와 2 * a * b가 같으면 a ⊕ b를 return 합니다.</p>
</blockquote>
<h4 id="🔷-풀이-1">🔷 풀이</h4>
<p><strong>- 1번째 풀이</strong></p>
<pre><code class="language-js">function solution(a, b) {
    const concat = Number(`${a}${b}`)
    const double = 2 * a * b

    return concat &gt; double ? concat
    : concat === double ? concat
    : double
}</code></pre>
<ul>
<li><code>concat === double</code>일 때 <code>concat</code>을 리턴하는 경우를 <code>concat &gt; double</code>와 함께 표현할 수 있었다. 문제 조건을 문장 그대로 작성하기 보다는, 조건을 보다 효율적이고 간결하게 표시할 수 있는 지 한 번 더 고민해야겠다.</li>
</ul>
<p><strong>- 2번째 풀이 (refactor)</strong></p>
<pre><code class="language-js">function solution(a, b) {
    const concat = Number(`${a}${b}`)
    const double = 2 * a * b

    return concat &gt;= double ? concat : double
}</code></pre>
<h4 id="🔶-다른-사람의-풀이-1">🔶 다른 사람의 풀이</h4>
<ul>
<li><code>Math.max()</code> 활용<pre><code class="language-js">function solution(a, b) {
  return Math.max(Number(`${a}${b}`), 2 * a * b)
}</code></pre>
</li>
<li>3일차에서 정리했던 <code>Math.max()</code>.. 떠오르지 않았다.</li>
</ul>
<hr />
<h3 id="n개-간격의-원소들">n개 간격의 원소들</h3>
<blockquote>
<p>정수 리스트 num_list와 정수 n이 주어질 때, num_list의 첫 번째 원소부터 마지막 원소까지 n개 간격으로 저장되어있는 원소들을 차례로 담은 리스트를 return하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이-2">🔷 풀이</h4>
<pre><code class="language-js">function solution(num_list, n) {
    let arr = [];

    for(let i = 0; i &lt; num_list.length; i += n) {
        arr.push(num_list[i])
    }

    return arr
}</code></pre>
<h4 id="🔶-다른-사람의-풀이-2">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">function solution(num_list, n) {
    return num_list.filter((_, i) =&gt; !(i % n))
}</code></pre>
<ul>
<li><code>_</code>: 사용하지 않는 매개변수 표현 (빈칸으로 두어도 되지만 헷갈릴 수 있으므로)</li>
<li>나머지 연산자를 활용해서 n번째 인덱스를 표현할 수 있다..!</li>
</ul>
<hr />
<h2 id="📝-필요-내용-정리">📝 필요 내용 정리</h2>
<h3 id="대소문자-변환-메서드">대소문자 변환 메서드</h3>
<ul>
<li><code>toUpperCase</code>: 대문자 변환</li>
<li><code>toLowerCase</code>: 소문자 변환</li>
<li>원본 문자열은 변경하지 않고, 새 문자열을 반환함<pre><code class="language-js">const original = &quot;HeLLo&quot;;
const lower = original.toLowerCase();
</code></pre>
</li>
</ul>
<p>console.log(original); // &quot;HeLLo&quot; (원본 그대로)
console.log(lower);    // &quot;hello&quot;  (새 문자열)</p>
<p>```</p>
<h3 id="findindex"><code>findIndex()</code></h3>
<ul>
<li>배열을 앞에서부터 순회하면서, 콜백 함수의 조건을 만족하는 <strong>첫 번째 요소의 인덱스</strong> 반환</li>
<li>없다면 <code>-1</code> 반환</li>
</ul>
<h2 id="🗂️-문제-목록-5개">🗂️ 문제 목록 (5개)</h2>
<p>n 번째 원소부터🏷️
두 수의 연산값 비교하기🏷️
대문자로 바꾸기
n개 간격의 원소들
첫 번째로 나오는 음수</p>