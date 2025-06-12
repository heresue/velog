<h2 id="🔎-주요-문제-풀이">🔎 주요 문제 풀이</h2>
<h3 id="하샤드-수">하샤드 수</h3>
<blockquote>
<p>양의 정수 x가 하샤드 수이려면 x의 자릿수의 합으로 x가 나누어져야 합니다. 예를 들어 18의 자릿수 합은 1+8=9이고, 18은 9로 나누어 떨어지므로 18은 하샤드 수입니다. 자연수 x를 입력받아 x가 하샤드 수인지 아닌지 검사하는 함수, solution을 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이">🔷 풀이</h4>
<p><strong>- 1번째 풀이: 숫자 풀이</strong></p>
<pre><code class="language-js">function solution(x) {
    let sum = 0;
    let num = x;

    while(num &gt; 0) {
        sum += num % 10;
        num = Math.floor(num / 10)
    }
    return x % sum === 0
}</code></pre>
<ul>
<li>숫자 풀이</li>
<li><code>for</code>문 보다 <code>while</code>문이 적절<ul>
<li>자리 개수(몇 번 반복할지)를 알 필요 없음. 숫자가 0이 될 때까지 나눠서 처리하면 됨 (조건식이 종료 조건 위주)</li>
<li><code>num</code>을 계속 10으로 나누며 자릿수를 자르고, <code>num === 0</code>이 되면 종료</li>
</ul>
</li>
</ul>
<p><strong>- 2번째 풀이: 문자 풀이</strong></p>
<pre><code class="language-js">function solution(x) {
    const sum = String(x).split('').reduce((acc, cur) =&gt; acc + Number(cur), 0)

    return x % sum === 0
}</code></pre>
<ul>
<li><code>reduce</code> 연산 시, 숫자로 변환하기!</li>
</ul>
<hr />
<h3 id="음양-더하기">음양 더하기</h3>
<blockquote>
<p>어떤 정수들이 있습니다. 이 정수들의 절댓값을 차례대로 담은 정수 배열 absolutes와 이 정수들의 부호를 차례대로 담은 불리언 배열 signs가 매개변수로 주어집니다. 실제 정수들의 합을 구하여 return 하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이-1">🔷 풀이</h4>
<pre><code class="language-js">function solution(absolutes, signs) {
    const num_list = absolutes.map((x, i) =&gt; signs[i] ? x : -x)

    let sum = 0;

    for(let i = 0; i &lt; num_list.length; i++) {
        sum += num_list[i]
    }

    return sum
}</code></pre>
<h4 id="🔶-다른-사람의-풀이">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">function solution(absolutes, signs) {
    return absolutes.reduce((acc, cur, i) =&gt; acc + (signs[i]? cur : -cur), 0)
}</code></pre>
<ul>
<li><code>reduce()</code> 활용</li>
</ul>
<h4 id="두-풀이-방식-비교">두 풀이 방식 비교</h4>
<table>
<thead>
<tr>
<th>구분</th>
<th>첫 번째 코드</th>
<th>두 번째 코드</th>
</tr>
</thead>
<tbody><tr>
<td>작성 방식</td>
<td><strong>map + for문</strong></td>
<td><strong>reduce()</strong></td>
</tr>
<tr>
<td>처리 흐름</td>
<td><ul><li>1단계: map으로 변환 (배열 생성)</li><li>2단계: for문으로 누적합</li></ul></td>
<td><ul><li>한 번에 누적합</li></ul></td>
</tr>
<tr>
<td>메모리 사용</td>
<td><code>num_list</code>라는 <strong>새로운 배열 생성</strong></td>
<td>배열 추가 생성 X (inline 계산)</td>
</tr>
<tr>
<td>가독성</td>
<td>조금 더 명시적 (단계 나눔)</td>
<td>좀 더 함수형 (한 줄 처리)</td>
</tr>
<tr>
<td>연산량</td>
<td>2번 순회 (map + for문)</td>
<td>1번 순회 (reduce만 사용)</td>
</tr>
<tr>
<td>성능</td>
<td>일반적으로 약간 더 느림 (배열 추가 생성 때문)</td>
<td>더 빠름 (순회 1번, 메모리 절약)</td>
</tr>
<tr>
<td>- <code>map + for</code>: 단계가 명확하여 디버깅, 가독성 측면에서 좋지만, 추가배열이 필요하여 메모리 사용 증가</td>
<td></td>
<td></td>
</tr>
<tr>
<td>- <code>reduce()</code>: 추가배열 생성 없이 바로 누적되어 메모리 효율성이 높고, 함수형 패턴으로 간결하게 작성 가능</td>
<td></td>
<td></td>
</tr>
</tbody></table>
<hr />
<h3 id="없는-숫자-더하기">없는 숫자 더하기</h3>
<blockquote>
<p>0부터 9까지의 숫자 중 일부가 들어있는 정수 배열 numbers가 매개변수로 주어집니다. numbers에서 찾을 수 없는 0부터 9까지의 숫자를 모두 찾아 더한 수를 return 하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이-2">🔷 풀이</h4>
<p><strong>- 1번째 풀이 (합 차이 패턴)</strong></p>
<pre><code class="language-js">function solution(numbers) {
    return 45 - numbers.reduce((acc, cur) =&gt; acc + cur, 0)
}</code></pre>
<ul>
<li>0부터 9까지의 숫자의 합은 <code>45</code></li>
<li>numbers에서 찾을 수 없는 숫자를 더한 수
= <code>45</code> - <code>numbers의 합</code></li>
</ul>
<p><strong>- 2번째 풀이 (명시적 탐색 패턴)</strong></p>
<pre><code class="language-js">function solution(numbers) {
    let answer = 0

    for (let i = 0; i &lt;= 9; i++) {
        if(!numbers.includes(i)) answer += i
    }

    return answer
}</code></pre>
<ul>
<li>문제에서는 숫자의 범위를 0~9로 했지만, 더 길어질 수 있다는 점을 고려하면 이 코드가 좀 더 활용도가 좋지 않을까 하는 생각이 든다. 물론 1번째 풀이에서 총합을 코드로 작성할 수도 있겠지만.. 총합을 계산하거나 작성하는 코드를 추가작성해야 한다는 점도 들 수 있겠다. 더불어 2번째 풀이가 요구사항을 좀 더 명시적으로 표현해서 의도가 명확하고 확장성이 좋은 것 같다.</li>
</ul>
<hr />
<h2 id="🗂️-문제-목록-5개">🗂️ 문제 목록 (5개)</h2>
<p>정수 내림차순으로 배치하기
정수 제곱근 판별
하샤드 수🏷️
음양 더하기🏷️
없는 숫자 더하기🏷️</p>