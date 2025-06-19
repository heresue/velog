<h2 id="🔎-주요-문제-풀이">🔎 주요 문제 풀이</h2>
<h3 id="배열-회전시키기">배열 회전시키기</h3>
<blockquote>
<p>정수가 담긴 배열 numbers와 문자열 direction가 매개변수로 주어집니다. 배열 numbers의 원소를 direction방향으로 한 칸씩 회전시킨 배열을 return하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이">🔷 풀이</h4>
<p><strong>- 1번째 풀이</strong></p>
<pre><code class="language-js">function solution(numbers, direction) {
    let answer = numbers.slice()

    if(direction === &quot;right&quot;) {
        answer.pop()
        answer.unshift(numbers.at(-1))
    } else {
        answer.shift()
        answer.push(numbers[0])
    }

    return answer
}</code></pre>
<ul>
<li>로직 구상<ul>
<li>numbers 배열을 복제: <code>slice()</code>
: <code>let answer = numbers</code>로 선언하면 이후 수정시 원본 배열도 함께 변경됨</li>
<li><code>direction === &quot;right&quot;</code> 일 경우, 마지막 요소를 제거하고, 배열의 첫 번째에 추가</li>
<li><code>direction === &quot;left&quot;</code> 일 경우, 첫번째 요소를 제거하고, 배열의 마지막에 추가</li>
</ul>
</li>
<li>원본 배열 보호 가능</li>
<li>단, 원본 배열인 numbers가 변경되는 경우 위험성 존재
(<code>answer</code> 배열 요소로 마지막 요소와 첫번째 요소를 변수로 선언해서 저장하면 원본 의존도를 없앨 수 있긴 함)</li>
</ul>
<p><strong>- 2번째 풀이 (refactor)</strong></p>
<pre><code class="language-js">function solution(numbers, direction) {
    if(direction === &quot;right&quot;) {
        numbers.unshift(numbers.pop())
    } else {
        numbers.push(numbers.shift())
    }
    return numbers
}</code></pre>
<ul>
<li>제거하는 요소를 바로 추가해버리기...!!!</li>
<li>원본 배열 변경</li>
<li>코드가 간결해지고, 불필요한 변수 선언 줄임</li>
</ul>
<hr />
<h3 id="핸드폰-번호-가리기">핸드폰 번호 가리기</h3>
<blockquote>
<p>프로그래머스 모바일은 개인정보 보호를 위해 고지서를 보낼 때 고객들의 전화번호의 일부를 가립니다.
전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 *으로 가린 문자열을 리턴하는 함수, solution을 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이-1">🔷 풀이</h4>
<pre><code class="language-js">function solution(phone_number) {
    const count = phone_number.length - 4
    const hide = &quot;*&quot;.repeat(count)

    return hide + phone_number.substring(count, phone_number.length)
}</code></pre>
<ul>
<li><code>substr</code>는 deprecated 되어 쓰지 않는 것을 권장하고,
<code>substring</code>과 <code>slice</code> 중 <code>slice</code>가 음수를 지원하므로 <code>slice</code>를 추천</li>
</ul>
<h4 id="🔶-다른-사람의-풀이">🔶 다른 사람의 풀이</h4>
<p><strong>- slice()를 사용하며, 더 간결한 코드</strong></p>
<pre><code class="language-js">function solution(phone_number) {
    return result = &quot;*&quot;.repeat(phone_number.length - 4) + phone_number.slice(-4);
}</code></pre>
<ul>
<li><code>slice(n)</code>: n번째 인덱스부터 끝까지 추출</li>
</ul>
<p><strong>- 배열 활용</strong></p>
<pre><code class="language-js">function solution(phone_number) {
    return [...phone_number].fill(&quot;*&quot;, 0 , phone_number.length-4).join(&quot;&quot;)
}</code></pre>
<ul>
<li><code>arr.fill(value, start, end)</code>
: 배열의 <code>start</code> 인덱스부터 <code>end</code> 직전까지 <code>value</code>로 채움</li>
</ul>
<hr />
<h2 id="📝-필요-내용-정리">📝 필요 내용 정리</h2>
<h3 id="배열에-숫자-알파벳-담아내기">배열에 숫자, 알파벳 담아내기</h3>
<h4 id="숫자-배열-1100">숫자 배열 (1~100)</h4>
<pre><code class="language-js">const arr = Array.from(Array(100), (_, i) =&gt; i + 1);

console.log(arr) = [1, 2, 3, 4, ... , 99, 100]</code></pre>
<h4 id="아스키코드를-이용한-문자-배열">아스키코드를 이용한 문자 배열</h4>
<ul>
<li><code>String.fromCharCode()</code>: 아스키코드 번호를 받아 문자열을 구성하는 함수</li>
</ul>
<p><strong>(1) 대문자 알파벳 배열</strong></p>
<pre><code class="language-js">const arr Array.from({ length: 26}, (v, i) =&gt; String.fromCharCode(i + 65));

console.log(arr) = ['A', 'B', 'C', ... 'Y', 'Z']</code></pre>
<p><strong>(2) 소문자 알파벳 배열</strong></p>
<pre><code class="language-js">const arr Array.from({ length: 26}, (v, i) =&gt; String.fromCharCode(i + 97));

console.log(arr) = ['a', 'b', 'c', ... 'y', 'z']</code></pre>
<h2 id="🗂️-문제-목록-4개">🗂️ 문제 목록 (4개)</h2>
<p>lv.0 (3개)
숫자 찾기
외계행성의 나이
배열 회전시키기</p>
<p>lv.1 (1개)
핸드폰 번호 가리기</p>