<h2 id="🔎-주요-문제-풀이">🔎 주요 문제 풀이</h2>
<h3 id="모스부호-1">모스부호 (1)</h3>
<blockquote>
<p>(문제내용)
머쓱이는 친구에게 모스부호를 이용한 편지를 받았습니다. 그냥은 읽을 수 없어 이를 해독하는 프로그램을 만들려고 합니다. 문자열 letter가 매개변수로 주어질 때, letter를 영어 소문자로 바꾼 문자열을 return 하도록 solution 함수를 완성해보세요.
모스부호는 다음과 같습니다.</p>
</blockquote>
<pre><code class="language-js">morse = { 
    '.-':'a','-...':'b','-.-.':'c','-..':'d','.':'e','..-.':'f',
    '--.':'g','....':'h','..':'i','.---':'j','-.-':'k','.-..':'l',
    '--':'m','-.':'n','---':'o','.--.':'p','--.-':'q','.-.':'r',
    '...':'s','-':'t','..-':'u','...-':'v','.--':'w','-..-':'x',
    '-.--':'y','--..':'z'
}</code></pre>
<h4 id="🔷-풀이">🔷 풀이</h4>
<pre><code class="language-js">function solution(letter) {
    const morse = { 
    '.-':'a','-...':'b','-.-.':'c','-..':'d','.':'e','..-.':'f',
    '--.':'g','....':'h','..':'i','.---':'j','-.-':'k','.-..':'l',
    '--':'m','-.':'n','---':'o','.--.':'p','--.-':'q','.-.':'r',
    '...':'s','-':'t','..-':'u','...-':'v','.--':'w','-..-':'x',
    '-.--':'y','--..':'z'
    }

    return letter.split(' ').map((code) =&gt; morse[code]).join('')
}</code></pre>
<h4 id="🔶-다른-사람의-풀이">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">function solution(letter) {
    const morse = { 
    '.-':'a','-...':'b','-.-.':'c','-..':'d','.':'e','..-.':'f',
    '--.':'g','....':'h','..':'i','.---':'j','-.-':'k','.-..':'l',
    '--':'m','-.':'n','---':'o','.--.':'p','--.-':'q','.-.':'r',
    '...':'s','-':'t','..-':'u','...-':'v','.--':'w','-..-':'x',
    '-.--':'y','--..':'z'
    }

    return letter.split(' ').reduce((acc, cur) =&gt; acc + morse[cur], '')
}</code></pre>
<ul>
<li><code>map</code> + <code>join</code>을 <code>reduce</code>로 한 큐에 처리하기..!</li>
</ul>
<hr />
<h3 id="2차원으로-만들기">2차원으로 만들기</h3>
<blockquote>
<p>정수 배열 num_list와 정수 n이 매개변수로 주어집니다. num_list를 다음 설명과 같이 2차원 배열로 바꿔 return하도록 solution 함수를 완성해주세요.
num_list가 [1, 2, 3, 4, 5, 6, 7, 8] 로 길이가 8이고 n이 2이므로 num_list를 2 * 4 배열로 다음과 같이 변경합니다. 2차원으로 바꿀 때에는 num_list의 원소들을 앞에서부터 n개씩 나눠 2차원 배열로 변경합니다.</p>
</blockquote>
<h4 id="🔷-풀이-1">🔷 풀이</h4>
<pre><code class="language-js">function solution(num_list, n) {
    let arr = []

    for(let i = 0; i &lt; num_list.length; i = i * n) { 
        arr.push(num_list.splice(i, n))
    }

    return arr
}</code></pre>
<h4 id="🔶-다른-사람의-풀이-1">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">function solution(num_list, n) {
    let arr = []

    while(num_list.length) { 
        arr.push(num_list.splice(0, n))
    }

    return arr
}</code></pre>
<ul>
<li><code>splice()</code>는 원본 배열을 자르기 때문에, 자르다보면 num_list가 빈 배열이 됨</li>
<li><blockquote>
<p>while의 조건으로 적용</p>
</blockquote>
<ul>
<li>참고: <code>slice()</code>의 경우는 원본 배열이 바뀌지 않음!</li>
</ul>
</li>
</ul>
<hr />
<h3 id="길이에-따른-연산">길이에 따른 연산</h3>
<blockquote>
<p>정수가 담긴 리스트 num_list가 주어질 때, 리스트의 길이가 11 이상이면 리스트에 있는 모든 원소의 합을 10 이하이면 모든 원소의 곱을 return하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이-2">🔷 풀이</h4>
<pre><code class="language-js">function solution(num_list) {
    return num_list.length &gt;= 11 ?
        num_list.reduce((acc, cur) =&gt; acc + cur, 0)
        : num_list.reduce((acc, cur) =&gt; acc * cur, 1)
}</code></pre>
<h4 id="🔶-다른-사람의-풀이-2">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">function solution(num_list) {
    return num_list.reduce((acc, cur) =&gt; num_list.length &gt; 10 ? acc + cur : acc * cur)
}</code></pre>
<ul>
<li>내 풀이와 같은 로직이지만, 조건문을 reduce 안에서 적용함으로써 코드가 더 간단해짐</li>
<li>하지만 reduce에 초기값이 설정되지 않아 오류 발생 가능성 있음</li>
<li>안정성 개선 코드 (초기값 명시)<pre><code class="language-js">function solution(num_list) {
    const isSum = num_list.length &gt; 10
  return num_list.reduce((acc, cur) =&gt; isSum ? acc + cur : acc * cur, isSum ? 0 : 1)
}</code></pre>
</li>
</ul>
<hr />
<h2 id="🗂️-문제-목록-6개">🗂️ 문제 목록 (6개)</h2>
<p>모스부호 (1)
2차원으로 만들기
A로 B 만들기
소문자로 바꾸기
원하는 문자열 찾기
길이에 따른 연산</p>