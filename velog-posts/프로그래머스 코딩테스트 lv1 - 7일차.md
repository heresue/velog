<h2 id="🔎-주요-문제-풀이">🔎 주요 문제 풀이</h2>
<h3 id="두-정수-사이의-합">두 정수 사이의 합</h3>
<blockquote>
<p>두 정수 a, b가 주어졌을 때 a와 b 사이에 속한 모든 정수의 합을 리턴하는 함수, solution을 완성하세요.
예를 들어 a = 3, b = 5인 경우, 3 + 4 + 5 = 12이므로 12를 리턴합니다.</p>
</blockquote>
<h4 id="🔷-풀이">🔷 풀이</h4>
<pre><code class="language-js">function solution(a, b) {
    const [min, max] = [a, b].sort((a, b) =&gt; a - b);
    let sum = 0;

    for(let i = min; i &lt;= max; i++) {
        sum += i;
    }

    return sum
}</code></pre>
<ul>
<li>min, max값을 정렬할 때 <code>Math.min</code>, <code>Math.max</code>를 이용해도 괜찮을 듯</li>
</ul>
<h4 id="🔶-다른-사람의-풀이">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">function solution(a, b) {
    const [min, max] = [a, b].sort((a, b) =&gt; a - b);
    const count = max - min + 1;

    return (min + max) * count / 2;
}</code></pre>
<ul>
<li>등차수열 공식 이용<ul>
<li>for문을 사용할 필요 없이 아주 간단한 코드로 구현 가능</li>
</ul>
</li>
</ul>
<hr />
<h3 id="문자열-내-p와-y의-개수">문자열 내 p와 y의 개수</h3>
<blockquote>
<p>대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True, 다르면 False를 return 하는 solution를 완성하세요. 'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다. 단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.
예를 들어 s가 &quot;pPoooyY&quot;면 true를 return하고 &quot;Pyy&quot;라면 false를 return합니다.</p>
</blockquote>
<h4 id="🔷-풀이-1">🔷 풀이</h4>
<p><strong>- 1번째 풀이</strong></p>
<pre><code class="language-js">function solution(s){
    const str = s.toLowerCase().split('')
    const count = (n) =&gt; {
        return str.filter((x) =&gt; x == n).length
    }

    if (!count(&quot;p&quot;) &amp;&amp; !count(&quot;y&quot;)) {
        return true
    } else if (count(&quot;p&quot;) === count(&quot;y&quot;)) {
        return true
    } else {
        return false
    }
}</code></pre>
<ul>
<li>굉장히 불필요하게 길어진 코드.. 좀 더 간략하게 리팩토링 해보자<ul>
<li>true, false값을 굳이 저렇게 return으로 출력하지 않도록</li>
</ul>
</li>
</ul>
<p><strong>- 2번째 풀이 (refactor)</strong></p>
<pre><code class="language-js">function solution(s){
    const str = s.toLowerCase().split('')
    const count = (n) =&gt; str.filter((x) =&gt; x === n).length

    return count(&quot;p&quot;) === count(&quot;y&quot;)
}</code></pre>
<h4 id="🔶-다른-사람의-풀이-1">🔶 다른 사람의 풀이</h4>
<p><strong>- split() 더 활용하기</strong></p>
<pre><code class="language-js">function solution(s){
    const count = (n) =&gt; (s.toLowerCase().split(n).length - 1);

    return count(&quot;p&quot;) === count(&quot;y&quot;);
}</code></pre>
<ul>
<li><code>split()</code>는 구분자를 기준으로 문자열을 쪼개어 배열을 반환한다.
<code>split(&quot;p&quot;)</code>을 하면, <code>&quot;p&quot;</code>을 기준으로 문자열이 쪼개져 배열을 반환하므로, <strong>반환된 배열의 길이</strong>는 <strong><code>&quot;p+1&quot;</code></strong>가 된다.</li>
<li><blockquote>
<p>즉, <code>&quot;p&quot;</code>의 개수 = <code>str.split(&quot;p&quot;).length - 1</code></p>
</blockquote>
</li>
</ul>
<p><strong>- reduce() 활용</strong></p>
<pre><code class="language-js">function solution(s){

    return [...s.toLowerCase()].reduce((acc, cur) =&gt; {
        if(cur ==='p') return acc + 1;
        else if(cur ==='y') return acc - 1;
        return acc;
    }, 0) ? false : true;
}</code></pre>
<ul>
<li>논리적인 비교를 수학적 연산으로 표현한 점이 놀랍다🫢</li>
</ul>
<h2 id="📝-필요-내용-정리">📝 필요 내용 정리</h2>
<h3 id="등차수열-등비수열">등차수열, 등비수열</h3>
<h4 id="등차수열">등차수열</h4>
<ul>
<li>n번째 항
<img alt="" src="https://velog.velcdn.com/images/heresue/post/b0f35d91-0268-4419-9d30-041020fecb76/image.png" /></li>
<li>수열의 합
<img alt="" src="https://velog.velcdn.com/images/heresue/post/66c44af1-71cf-472e-bb62-aafd741a27a6/image.png" /><pre><code class="language-js">const num_list = [2, 5, 8, 11, 14];
</code></pre>
</li>
</ul>
<p>// 공차
const d = num_list[1] - num_list[0];
// 항의 개수
const n = num_list.length;</p>
<p>// n번째 항
const num = num_list[0] + (n - 1) * d</p>
<p>// num_list 배열의 합
const sum = (num_list[0] + num_list[n - 1]) * n / 2;</p>
<pre><code>
#### 등비수열
- n번째 항
![](https://velog.velcdn.com/images/heresue/post/ab88138d-500a-471a-8a22-09766d8880ac/image.png)
- 수열의 합
![](https://velog.velcdn.com/images/heresue/post/7ee3788f-ced0-4583-a27c-81c3b31f4a49/image.png)
```js
const num_list = [3, 6, 12, 24, 48];

// 공비
const r = num_list[1] / num_list[0]; // 2
// 항의 개수
const n = num_list.length;

// n번째 항
const num = num_list[0] * (r ** (n - 1))

// num_list 배열의 합
const sum = num_list[0] * (1 - r ** n) / (1 - r)</code></pre><hr />
<h2 id="🗂️-문제-목록-5개">🗂️ 문제 목록 (5개)</h2>
<p>x만큼 간격이 있는 n개의 숫자
나머지가 1이 되는 수 찾기
문자열을 정수로 바꾸기
두 정수 사이의 합🏷️
문자열 내 p와 y의 개수🏷️</p>