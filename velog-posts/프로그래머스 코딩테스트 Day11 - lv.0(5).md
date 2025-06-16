<h2 id="🔎-주요-문제-풀이">🔎 주요 문제 풀이</h2>
<h3 id="주사위의-개수">주사위의 개수</h3>
<blockquote>
<p>머쓱이는 직육면체 모양의 상자를 하나 가지고 있는데 이 상자에 정육면체 모양의 주사위를 최대한 많이 채우고 싶습니다. 상자의 가로, 세로, 높이가 저장되어있는 배열 box와 주사위 모서리의 길이 정수 n이 매개변수로 주어졌을 때, 상자에 들어갈 수 있는 주사위의 최대 개수를 return 하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이">🔷 풀이</h4>
<pre><code class="language-js">function solution(box, n) {
    let count = 1;

    box.forEach(x =&gt; {
        count *= Math.floor(x / n)
    })

    return count
}</code></pre>
<h4 id="🔶-다른-사람의-풀이">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">function solution(box, n) {
    return box.reduce((acc, cur) =&gt; acc * Math.floor(cur / n), 1)
}</code></pre>
<ul>
<li>reduce 활용</li>
<li>덧셈 연산일 때는 reduce가 잘 떠올랐는데, 곱셈으로 바뀌니까 생각나지 않았다. 다시 한 번 리마인드</li>
</ul>
<hr />
<h3 id="최댓값-만들기-2">최댓값 만들기 (2)</h3>
<blockquote>
<p>정수 배열 numbers가 매개변수로 주어집니다. numbers의 원소 중 두 개를 곱해 만들 수 있는 최댓값을 return하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이-1">🔷 풀이</h4>
<pre><code class="language-js">function solution(numbers) {
    const arr = numbers.sort((a, b) =&gt; a - b)

    return Math.max(arr[0] * arr[1], arr.at(-1) * arr.at(-2))
}</code></pre>
<ul>
<li>음수가 포함된 최댓값 만들기. 처음 로직을 구상할 때 아주아주 어렵게 생각해서 꼬여버렸다. 단순하게 오름차순으로 정렬해서, 처음 두 값과 마지막 두 값을 곱하고 비교하면 되는데.. 부호가 같은 경우를 조건으로 나누려고 했었고 그래서 아주 복잡하고 비효율적인 코드가 작성됐다. 그건 여기에 쓸 필요도 없을 것 같아서 바로 삭제...!</li>
<li>만약 at() 메서드를 몰랐다면?
arr.[arr.length - 1] 이런식으로도 쓸 수 있겠다.</li>
<li>인자로 들어온 numbers를 <code>sort</code>한 배열은 arr로 할당할 필요없이 바로 재할당해줘도 된다.
<code>numbers = numbers.sort(...)</code><ul>
<li>다만, 이런 경우 원본 배열을 바꾸기 때문에 문제풀이에서는 괜찮지만, 실무에서는 풀이처럼 변수에 담아 복사본을 만들자. </li>
</ul>
</li>
</ul>
<hr />
<h2 id="📝-필요-내용-정리">📝 필요 내용 정리</h2>
<h3 id="isnan-numberisnan">isNaN(), Number.isNaN()</h3>
<h4 id="nan">NaN</h4>
<ul>
<li>Not-A-Number, 숫자가 아닌 값</li>
<li>기본적으로 number type으로 분류</li>
<li><code>NaN</code>은 비교 연산자(<code>==</code>, <code>===</code>)를 사용해서 판별할 수 없음<ul>
<li><code>Nan == NaN</code>, <code>NaN === NaN</code> // false</li>
</ul>
</li>
<li>어떤 값이 NaN인지 판별하고 싶다면? <strong><code>isNan()</code>, <code>Number.isNaN()</code></strong></li>
</ul>
<h4 id="isnan">isNan()</h4>
<ul>
<li>매개변수를 숫자로 변환하여 판단<ul>
<li>빈 문자열, boolean과 같이 숫자값으로 변환되는 경우 예상치 못한 값을 얻을 수 있음</li>
</ul>
</li>
<li>isNaN()이 <code>true</code>라면?</li>
<li><blockquote>
<p>숫자가 아니거나, 변환이 실패해서 NaN이 된 경우</p>
</blockquote>
</li>
<li>isNan()이 <code>false</code>라면?</li>
<li><blockquote>
<p>숫자이거나, 숫자로 변환 가능한 값</p>
</blockquote>
</li>
</ul>
<h4 id="numberisnan-권장">Number.isNaN() (권장)</h4>
<ul>
<li>매개변수를 숫자로 변환하지 않음</li>
<li><blockquote>
<p>숫자가 아닌 값일 경우, false 반환</p>
</blockquote>
</li>
<li>Number.isNaN()이 <code>true</code>라면?</li>
<li><blockquote>
<p>값이 정확히 <code>NaN</code></p>
</blockquote>
<ul>
<li>숫자 타입이지만 잘못된 숫자 결과 (계산 불능)</li>
<li>ex: <code>NaN</code></li>
</ul>
</li>
<li>Number.isNan()이 <code>false</code>라면?</li>
<li><blockquote>
<p><code>NaN</code>이 아님</p>
</blockquote>
<ul>
<li>타입이 숫자인 경우 / 타입이 숫자가 아닌 경우, <code>undefined</code>, <code>{}</code> 등</li>
</ul>
</li>
</ul>
<pre><code class="language-js">// 아래 매개변수를 Number.isNaN()에 적용하면 모두 false 반환
isNaN(&quot;NaN&quot;);     // true
isNaN(undefined); // true
isNaN({});        // true
isNaN(&quot;blabla&quot;);  // true
isNaN(true);      // false, 1로 강제 변환
isNaN(null);      // false, 0으로 강제 변환
isNaN(&quot;37&quot;);      // false, 37로 강제 변환
isNaN(&quot;37.37&quot;);   // false, 37.37로 강제 변환
isNaN(&quot;&quot;);        // false, 0으로 강제 변환
isNaN(&quot; &quot;);       // false, 0으로 강제 변환</code></pre>
<h4 id="숫자인지-확실하게-판별하고-싶다면">숫자인지 확실하게 판별하고 싶다면?</h4>
<pre><code class="language-js">typeof value === 'number' &amp;&amp; !Number.isNaN(value)</code></pre>
<hr />
<h3 id="절대값">절대값</h3>
<ul>
<li><code>Math.abs()</code></li>
<li>문자열을 넣을 경우<ul>
<li>내부적으로 <code>Number()</code>로 타입을 숫자로 변환 후, 동작</li>
<li>변환 불가한 문자열은 <code>NaN</code> 반환</li>
</ul>
</li>
<li>배열을 넣을 경우<ul>
<li>내부적으로 문자열로 변환한 다음 <code>Number()</code> 적용</li>
</ul>
</li>
<li>객체: <code>NaN</code> 반환<pre><code class="language-js">console.log(Math.abs(&quot;10&quot;));  // 10 (문자열 → 숫자로 변환)
console.log(Math.abs(&quot;-10&quot;)); // 10
console.log(Math.abs(&quot;abc&quot;)); // NaN
console.log(Math.abs([10]));  // 10
console.log(Math.abs([&quot;10&quot;]));  // 10
console.log(Math.abs([1,2]));  // NaN
console.log(Math.abs({}));  // NaN</code></pre>
</li>
</ul>
<hr />
<h2 id="🗂️-문제-목록-4개">🗂️ 문제 목록 (4개)</h2>
<p>주사위의 개수🏷️
문자열 정렬하기 (1)
숨어있는 숫자의 덧셈 (1)
최댓값 만들기 (2)🏷️</p>
<hr />
<h2 id="comment">Comment</h2>
<p>lv.1 문제를 풀다가, 며칠 전 lv.0의 정답률 낮은 문제인 최빈값을 푼 후로는 lv.0의 낮은 정답률 문제를 먼저 짚고 넘어가야겠다는 생각이 들었다. 그런데 낮은 정답률 문제를 풀면 머리가 너무 지끈거려서 컨디션이 급격하게 떨어진다......ㅎ
좀 나아질까? 하는 생각으로 며칠 진행한 결과, 일단은 정답률 높은 순부터 순차적으로 푸는게 나을 것 같다고 다시 결론을 내렸다. 메서드나 함수를 더 많이 접하고, 좀 더 사고력을 기르면서 진행해야할 것 같다.
오늘도 사실 5개를 풀었지만.. 낮은 정답률 문제 하나는 양심상 제외했다. 나중에 다시 풀어보기로..(아마 처음 접하는 느낌이 나지 않을까? ㅎ)</p>