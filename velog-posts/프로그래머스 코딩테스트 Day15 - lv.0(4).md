<h2 id="🔎-주요-문제-풀이">🔎 주요 문제 풀이</h2>
<h3 id="369게임">369게임</h3>
<blockquote>
<p>머쓱이는 친구들과 369게임을 하고 있습니다. 369게임은 1부터 숫자를 하나씩 대며 3, 6, 9가 들어가는 숫자는 숫자 대신 3, 6, 9의 개수만큼 박수를 치는 게임입니다. 머쓱이가 말해야하는 숫자 order가 매개변수로 주어질 때, 머쓱이가 쳐야할 박수 횟수를 return 하도록 solution 함수를 완성해보세요.</p>
</blockquote>
<h4 id="🔷-풀이">🔷 풀이</h4>
<p><strong>- 1번째 풀이</strong></p>
<pre><code class="language-js">function solution(order) {
    return [...String(order)].filter(x =&gt; x === '3' || x === '6' || x === '9').length
}</code></pre>
<h4 id="🔶-다른-사람의-풀이">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">function solution(order) {
    const orderSet = new Set([3, 6, 9])

    return [...String(order)].filter((num) =&gt; orderSet.has(Number(num))).length
}</code></pre>
<h2 id="📝-필요-내용-정리">📝 필요 내용 정리</h2>
<h3 id="set">Set</h3>
<p><strong>중복 없는 유일한 값들의 집합을 저장할 수 있는 자료구조</strong>
(배열처럼 보이지만 동작 방식과 특징이 다름)</p>
<h4 id="특징">특징</h4>
<ul>
<li>중복 허용 X</li>
<li>삽입한 순서대로 저장되어 순서 유지</li>
<li>숫자, 문자열, 객체, 배열 등 모두 저장 가능<pre><code class="language-js">const mySet = new Set();
</code></pre>
</li>
</ul>
<p>mySet.add(1);
mySet.add(2);
mySet.add(2);  // 중복된 값은 무시됨</p>
<p>console.log(mySet); // Set(2) { 1, 2 }</p>
<pre><code>#### 주요 메서드
- `add(value)`: 값 추가
- `has(value)`: 값이 존재하는지 확인 (boolean)
  - `includes()` 보다 빠르고 효율적
- `delete(value)`: 값 제거
- `clear()`: 모든 요소 제거
```js
// has(value)
const digitSet = new Set([3, 6, 9]);
digitSet.has(6); // true</code></pre><h2 id="🗂️-문제-목록-4개">🗂️ 문제 목록 (4개)</h2>
<p>369게임
합성수 찾기
중복된 문자 제거
숨어있는 숫자의 덧셈 (1)</p>