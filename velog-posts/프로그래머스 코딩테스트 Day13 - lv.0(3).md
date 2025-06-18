<h2 id="🔎-주요-문제-풀이">🔎 주요 문제 풀이</h2>
<h3 id="문자열-정렬하기-2">문자열 정렬하기 (2)</h3>
<blockquote>
<p>영어 대소문자로 이루어진 문자열 my_string이 매개변수로 주어질 때, my_string을 모두 소문자로 바꾸고 알파벳 순서대로 정렬한 문자열을 return 하도록 solution 함수를 완성해보세요.</p>
</blockquote>
<h4 id="🔷-풀이">🔷 풀이</h4>
<p><strong>- 1번째 풀이</strong></p>
<pre><code class="language-js">function solution(my_string) {
    return [...my_string].map((x) =&gt; x.toLowerCase()).sort()
}</code></pre>
<ul>
<li>개선할 점<ul>
<li>문자열을 우선 소문자로 변환 후, <code>split()</code>로 배열 변환하기
(더 빠르고 효율적)</li>
</ul>
</li>
</ul>
<p><strong>- 2번째 풀이 (refactor)</strong></p>
<pre><code class="language-js">function solution(my_string) {
    return my_string.toLowerCase().split('').sort().join('')
}</code></pre>
<p><strong>- 3번째 풀이 (refactor)</strong></p>
<pre><code class="language-js">function solution(my_string) {
    return [...my_string.toLowerCase()].sort().join('')
}</code></pre>
<ul>
<li><strong>문자열 변환 비교 (<code>split()</code> VS. <code>[...str]</code>)</strong><ul>
<li><code>split('')</code><ul>
<li>문자열 분리용 메서드</li>
<li>레거시 지원 (오래된 표준 메서드이기 때문에 안정적)</li>
<li>이모지, 복합 유니코드 등에서 이슈 발생 가능<ul>
<li>UTF-16 코드 유닛 단위로 분리 → 복합문자 깨질 수 있음</li>
</ul>
</li>
</ul>
</li>
<li><code>[...str]</code><ul>
<li>ES6 전개 연산자로, 이터러블을 순회</li>
<li>일부 구형 환경에서는 지원이 부족할 수 있음</li>
<li>코드포인트 단위 처리로, 이모지, 복합 유니코드 등에서 안전</li>
</ul>
</li>
<li>속도 및 성능 차이<ul>
<li>대부분의 브라우저에서는 <code>split()</code>이 약간 더 빠르지만 차이는 거의 미미함.
(수백MB 이상의 대용량 문자열에서만 체감되는 정도)</li>
</ul>
</li>
<li>성능 차이는 거의 없으므로, 브라우저 환경이나 이모지/유니코드 안전성 여부에 따라 결정<ul>
<li>일반 문자열 분리 -&gt; <code>split()</code></li>
<li>유니코드 안전성 필요 (이모지 등) -&gt; <code>[...str]</code><pre><code class="language-js">const emoji = '👍🏻';
console.log(emoji.split(''));  // ['👍','🏻']  → 분리됨 (코드 유닛 단위)
console.log([...emoji]);       // ['👍🏻']  → 올바르게 하나로 처리됨</code></pre>
</li>
</ul>
</li>
</ul>
</li>
</ul>
<hr />
<h2 id="🗂️-문제-목록-3개">🗂️ 문제 목록 (3개)</h2>
<p>피자 나눠 먹기 (2)
가장 큰 수 찾기
문자열 정렬하기 (2)</p>