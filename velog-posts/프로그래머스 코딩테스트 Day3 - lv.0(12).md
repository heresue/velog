<h2 id="🔎-주요-문제-풀이">🔎 주요 문제 풀이</h2>
<h3 id="배열의-유사도">배열의 유사도</h3>
<blockquote>
<p>두 배열이 얼마나 유사한지 확인해보려고 합니다. 문자열 배열 s1과 s2가 주어질 때 같은 원소의 개수를 return하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이">🔷 풀이</h4>
<pre><code class="language-js">  function solution(s1, s2) {
    return s1.filter((x) =&gt; s2.includes(x)).length;
}</code></pre>
<ul>
<li>배열을 문자열로 변환할 필요 없음</li>
<li>배열의 요소가 문자열일 때도 그대로 비교 가능</li>
</ul>
<hr />
<h3 id="순서쌍의-개수-약수-구하기">순서쌍의 개수 (약수 구하기)</h3>
<blockquote>
<p>순서쌍이란 두 개의 숫자를 순서를 정하여 짝지어 나타낸 쌍으로 (a, b)로 표기합니다. 자연수 n이 매개변수로 주어질 때 두 숫자의 곱이 n인 자연수 순서쌍의 개수를 return하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이-1">🔷 풀이</h4>
<p><strong>- 1번째 풀이 (오답)</strong></p>
<pre><code class="language-js">  function solution(n) {
    let i = 1;
    let arr = [];

    while(i &lt;= n) {
      arr = Number.isInteger(n / i);
    }

    return arr.length;
}</code></pre>
<ul>
<li><strong><code>while</code> 무한루프</strong><ul>
<li><code>i</code>값을 증가시키지 않아서 조건 <code>i &lt;= n</code>이 계속 true인 상태</li>
</ul>
</li>
<li><code>n</code>이 <code>i</code>로 나누어떨어지는 지를 확인했지만, <strong>결과를 배열에 누적하지 않음</strong></li>
<li><strong><code>while</code>문 대신 <code>for</code>문을 사용하는 것이 적절</strong><ul>
<li><strong>1부터 n까지 순회하는 고정 반복 구조</strong>
: 반복 범위가 고정된 경우, <code>for</code>문이 가독성이 좋고 실수할 여지가 적음</li>
<li><strong>루프 변수 선언, 조건문, 증가식을 한 줄에 명확히 작성할 수 있음</strong></li>
<li><code>while</code>문은 종료 조건이 명확하지 않거나, 내부에서 복잡한 흐름을 제어할 때 주로 사용</li>
</ul>
</li>
</ul>
<p><strong>- 2번째 풀이</strong></p>
<pre><code class="language-js">  function solution(n) {
      let arr = [];

      for(let i = 1; i &lt;= n; i++) {
          if(Number.isInteger(n / i)) {
              arr.push(i);
          }
      }

      return arr.length
  }</code></pre>
<h4 id="🔶-다른-사람의-풀이">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">  function solution(n) {
    return Array(n)
      .fill(1)
      .map((v,idx) =&gt; v + idx)
      .filter(v =&gt; n % v === 0)
      .length
}</code></pre>
<ul>
<li><p>1부터 n까지 순회하면서 n의 약수를 찾고, 개수를 반환하는 로직</p>
</li>
<li><blockquote>
<p><code>map</code>과 <code>filter</code>의 이해..!</p>
</blockquote>
</li>
<li><p><code>Array(n)</code></p>
<ul>
<li>길이 <code>n</code>의 배열 만들기<ul>
<li>ex: <code>n = 5</code> -&gt; <code>[empty x 5]</code></li>
</ul>
</li>
</ul>
</li>
<li><p><code>.fill(1)</code></p>
<ul>
<li>배열의 모든 값을 <code>1</code>로 채움</li>
<li>결과: <code>[1, 1, 1, 1, 1]</code></li>
</ul>
</li>
<li><p><code>.map((v, idx) =&gt; v + idx)</code></p>
<ul>
<li>각 요소에 인덱스를 더함<ul>
<li><code>v = 1</code>, <code>idx = 0, 1, 2, 3, 4</code></li>
<li>결과: <code>[1 + 0, 1 + 1, 1 + 2, 1 + 3, 1 +4]</code></li>
<li><blockquote>
<p><code>[1, 2, 3, 4, 5]</code></p>
</blockquote>
</li>
</ul>
</li>
<li>즉, <code>1</code>부터 <code>n</code>까지의 숫자 배열 생성</li>
</ul>
</li>
<li><p><code>for</code>문, <code>while</code>문 더 많이 연습해야겠다.
배열을 만드는 여러가지 방식..!
<code>map</code>을 활용할 수 있는지 고려하기 ★</p>
</li>
</ul>
<hr />
<h3 id="배열-원소의-길이">배열 원소의 길이</h3>
<blockquote>
<p>문자열 배열 strlist가 매개변수로 주어집니다. strlist 각 원소의 길이를 담은 배열을 return하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이-2">🔷 풀이</h4>
<pre><code class="language-js">  function solution(strlist) {
      let lengthArr = [];

      for(let i = 0; i &lt; strlist.length; i++) {
          const strLength = strlist[i].length
          lengthArr.push(strLength)
      }

      return lengthArr
  }</code></pre>
<h4 id="🔶-다른-사람의-풀이-1">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">  function solution(strlist) {
      return strlist.map((str) =&gt; str.length)
  }</code></pre>
<ul>
<li><code>map()</code>을 잘 활용하자..!</li>
</ul>
<hr />
<h3 id="더-크게-합치기">더 크게 합치기</h3>
<blockquote>
<p>연산 ⊕는 두 정수에 대한 연산으로 두 정수를 붙여서 쓴 값을 반환합니다. 예를 들면 다음과 같습니다.
12 ⊕ 3 = 123
3 ⊕ 12 = 312
양의 정수 a와 b가 주어졌을 때, a ⊕ b와 b ⊕ a 중 더 큰 값을 return 하는 solution 함수를 완성해 주세요.
단, a ⊕ b와 b ⊕ a가 같다면 a ⊕ b를 return 합니다.</p>
</blockquote>
<h4 id="🔷-풀이-3">🔷 풀이</h4>
<pre><code class="language-js">  function solution(a, b) {
      const strA = String(a)
      const strB = String(b)

      const arr = [strA + strB, strB + strA]
      const sortArr = arr.map(Number).sort((a, b) =&gt; b - a)

      return sortArr[0]
  }</code></pre>
<ul>
<li>문자열로 변환해서 배열에 담아, 전체를 숫자로 변환 후 정렬하는 로직을 생각했으나, 너무 복잡하게 생각한 것 같다. 굳이 배열로....? ㅎ</li>
</ul>
<h4 id="🔶-다른-사람의-풀이-2">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">  function solution(a, b) {
      return Math.max(Number(`${a}${b}`), Number(`${b}${a}`))
  }</code></pre>
<ul>
<li>벡틱을 활용한 문자열 합치기...!</li>
</ul>
<hr />
<h3 id="문자열-곱하기">문자열 곱하기</h3>
<blockquote>
<p>문자열 my_string과 정수 k가 주어질 때, my_string을 k번 반복한 문자열을 return 하는 solution 함수를 작성해 주세요.</p>
</blockquote>
<h4 id="🔷-풀이-4">🔷 풀이</h4>
<pre><code class="language-js">  function solution(my_string, k) {
      return my_string.repeat(k)
  }</code></pre>
<h4 id="🔶-다른-사람의-풀이-3">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">  function solution(my_string, k) {
      let result = '';

      for(let i = 0; i &lt; k; i++) {
          result += my_string;
      }

      return result;
  }</code></pre>
<ul>
<li>메서드로 간단하게 풀 수 있지만, for문으로 하는 연습 더 해보기</li>
<li>증감연산자 익숙해지기</li>
</ul>
<hr />
<h2 id="📝-필요-내용-정리">📝 필요 내용 정리</h2>
<h3 id="mathmax">Math.max()</h3>
<ul>
<li><p>가장 큰 값 반환하기</p>
</li>
<li><p><strong>배열</strong>은 직접 받을 수 없으므로, <strong>스프레드 연산자</strong>로 펼쳐서 전달</p>
<pre><code class="language-js">Math.max(3, 7, 2); // 7

const arr = [1, 5, 9];
Math.max(...arr); // 9</code></pre>
</li>
</ul>
<h3 id="문자열-자르기-메서드">문자열 자르기 메서드</h3>
<ul>
<li><code>split()</code>: 문자열을 특정 구분자 기준으로 나누어 <strong>배열로 변환</strong></li>
<li><code>slice(start, end)</code>: 문자열의 일부를 잘라서 반환<ul>
<li><code>end</code>는 포함되지 않음<pre><code class="language-js">&quot;abcdef&quot;.slice(0, 3); // &quot;abc&quot;
&quot;abcdef&quot;.slice(2); // &quot;cdef&quot;</code></pre>
</li>
</ul>
</li>
<li><code>substring(start, end)</code>: <code>slice()</code>와 비슷하지만 음수는 0으로 처리</li>
</ul>
<hr />
<h2 id="🗂️-문제-목록-12개">🗂️ 문제 목록 (12개)</h2>
<p>배열의 유사도🏷️
순서쌍의 개수🏷️
n의 배수 고르기
배열 원소의 길이🏷️
아이스 아메리카노
공배수
더 크게 합치기🏷️
<del>문자열 붙여서 출력하기</del>(node.js 입출력)
문자 리스트를 문자열로 변환하기
flag에 따라 다른 값 반환하기
n의 배수
문자열 곱하기🏷️
문자열의 앞의 n글자</p>