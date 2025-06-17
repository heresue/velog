<h2 id="🔎-주요-문제-풀이">🔎 주요 문제 풀이</h2>
<h3 id="분수의-덧셈">분수의 덧셈</h3>
<blockquote>
<p>첫 번째 분수의 분자와 분모를 뜻하는 numer1, denom1, 두 번째 분수의 분자와 분모를 뜻하는 numer2, denom2가 매개변수로 주어집니다. 두 분수를 더한 값을 기약 분수로 나타냈을 때 분자와 분모를 순서대로 담은 배열을 return 하도록 solution 함수를 완성해보세요.</p>
</blockquote>
<h4 id="🔷-풀이">🔷 풀이</h4>
<p><strong>- 1번째 풀이 (while문, for문)</strong></p>
<pre><code class="language-js">function solution(numer1, denom1, numer2, denom2) {
    let numer, denom
    if (denom1 === denom2) {
        numer = numer1 + numer2
        denom = denom1
    } else {
        // 분모 최소공배수 찾기
        let LCM = 1
        while(true) {
            if ((LCM % denom1 === 0) &amp;&amp; (LCM % denom2 === 0)) {
                break
            } 
            LCM++
        }

        denom = LCM

        numer1 = (denom / denom1) * numer1
        numer2 = (denom / denom2) * numer2
        numer = numer1 + numer2

        // 분자 최대공약수 찾기
        let GCD = 1
        for(let i = 2; i &lt;= Math.min(numer, denom); i++) {
            if((numer % i === 0) &amp;&amp; (denom % i === 0)) {
                GCD = i
            }
        }

        // 약분
        numer = numer / GCD
        denom = denom / GCD
    }

    return [numer, denom]
}</code></pre>
<ul>
<li>최소공배수(LCM)와 최대공약수(GCD)를 완전탐색 방식으로 찾아 느리고 비효율적임</li>
</ul>
<p><strong>- 2번째 풀이 (유클리드 호제법)</strong></p>
<pre><code class="language-js">function solution(numer1, denom1, numer2, denom2) {
    let numer, denom

    function GCD(a, b) {
        if (b === 0) return a
        return GCD(b, a % b)
    }

    function LCM(a, b) {
        return (a * b) / GCD(a, b)
    }

    if (denom1 === denom2) {
        numer = numer1 + numer2
        denom = denom1
    } else {
        denom = LCM(denom1, denom2);
        numer = (denom / denom1) * numer1 + (denom / denom2) * numer2;
    }
    const gcd = GCD(numer, denom);
    numer = numer / gcd;
    denom = denom / gcd;

    return [numer, denom];
}</code></pre>
<ul>
<li>개선할 점<ul>
<li>if문으로 나눌 필요가 없음</li>
</ul>
</li>
</ul>
<p><strong>- 3번째 풀이 (유클리드 호제법 &amp; if문 통합)</strong></p>
<pre><code class="language-js">function solution(numer1, denom1, numer2, denom2) {
    // 최대공약수
    function GCD(a, b) {
        if (b === 0) return a
        return GCD(b, a % b)
    }

    // 최소공배수
    function LCM(a, b) {
        return (a * b) / GCD(a, b)
    }

    let denom = LCM(denom1, denom2);
    let numer = (denom / denom1) * numer1 + (denom / denom2) * numer2;

    // 최종 분수 약분
    const gcd = GCD(numer, denom);
    numer = numer / gcd;
    denom = denom / gcd;

    return [numer, denom];
}</code></pre>
<hr />
<h3 id="암호-해독">암호 해독</h3>
<blockquote>
<p>군 전략가 머쓱이는 전쟁 중 적군이 다음과 같은 암호 체계를 사용한다는 것을 알아냈습니다.
암호화된 문자열 cipher를 주고받습니다.
그 문자열에서 code의 배수 번째 글자만 진짜 암호입니다.
문자열 cipher와 정수 code가 매개변수로 주어질 때 해독된 암호 문자열을 return하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이-1">🔷 풀이</h4>
<p><strong>- 1번째 풀이</strong></p>
<pre><code class="language-js">function solution(cipher, code) {
    const arr = [...cipher]
    let num_list = []

    for(let i = 1; i * code &lt;= arr.length; i++) {
        num_list.push(arr[i * code - 1])
    }

    return num_list.join('')
}</code></pre>
<ul>
<li>반복문 조건 주의: <code>i</code> 범위<ul>
<li><code>(i * code - 1)</code>가 arr의 인덱스 범위 안에 있어야 함</li>
<li><code>for</code>문의 조건: <code>i &lt; arr.length</code> (X)</li>
</ul>
</li>
</ul>
<p><strong>- 2번째 풀이</strong></p>
<pre><code class="language-js">function solution(cipher, code) {
    let result = ''

    for(let i = code - 1; i &lt; cipher.length; i += code) {
        result += cipher[i]
    }

    return result
}</code></pre>
<ul>
<li>index를 활용해서 좀 더 깔끔하게 작성 가능</li>
<li>배열을 만들 필요 없음</li>
</ul>
<h4 id="🔶-다른-사람의-풀이">🔶 다른 사람의 풀이</h4>
<pre><code class="language-js">function solution(cipher, code) {
    return [...cipher].filter((_, i) =&gt; (i + 1) % code === 0).join('')
}</code></pre>
<hr />
<h3 id="약수-구하기">약수 구하기</h3>
<blockquote>
<p>정수 n이 매개변수로 주어질 때, n의 약수를 오름차순으로 담은 배열을 return하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이-2">🔷 풀이</h4>
<p><strong>- 1번째 풀이</strong></p>
<pre><code class="language-js">function solution(n) {
    return Array(n).fill(1).map((x, i) =&gt; x + i).filter((x) =&gt; n % x === 0)
}</code></pre>
<p><strong>- 2번째 풀이</strong></p>
<pre><code class="language-js">function solution(n) {
    let i = 1
    let answer = []

    while(i &lt;= n) {
        if(n % i === 0) answer.push(i)
        i++
    }

    return answer
}</code></pre>
<p><strong>- 3번째 풀이 (시간복잡도 개선)</strong></p>
<pre><code class="language-js">function solution(n) {
    let answer = []

    for(let i = 1; i &lt;= Math.sqrt(n); i++) {
        if(n % i === 0) {
            answer.push(i)
            if (i !== n / i) answer.push(n / i)
        }
    }

    return answer.sort((a, b) =&gt; a - b)
}</code></pre>
<ul>
<li>약수는 쌍으로 존재한다는 특성을 활용</li>
</ul>
<hr />
<h2 id="📝-필요-내용-정리">📝 필요 내용 정리</h2>
<h3 id="유클리드-호제법-최대공약수-최소공배수">유클리드 호제법 (최대공약수, 최소공배수)</h3>
<h4 id="--최대공약수-gcd">- 최대공약수 (GCD)</h4>
<p><em>&quot;2개의 자연수 <code>a</code>, <code>b</code> (<code>a &gt; b</code>)에 대해서 <code>a</code>를 <code>b</code>로 나눈 나머지가 <code>r</code>일 때, <code>a</code>와 <code>b</code>의 최대공약수는 <code>b</code>와 <code>r</code>의 최대공약수와 같다.&quot;</em></p>
<ul>
<li>어떤 두 수 <code>a</code>, <code>b</code> (<code>a &gt;= b</code>)가 있을 때,
<code>GCD(a, b) = GCD(b, a % b)</code>를 반복하다가
<code>b</code>가 0이 되는 순간 <code>a</code>가 최대공약수가 됨<pre><code class="language-js">// 재귀방식
function GCD(a, b) {
  if (b === 0) return a;
  return GCD(b, a % b);
}
</code></pre>
</li>
</ul>
<p>// 삼항연산자
function GCD(a, b) {
    return b === 0 ? a : GCD(b, a % b);
}</p>
<p>// while문
function GCD(a, b) {
  let r
  while (b != 0) {
    r = a % b
    a = b
    b = r
  }
  return a
}</p>
<pre><code>#### - 최소공배수 (LCM)
두 수 `a`와 `b`의 최소공배수는 `a * b`를 `a와 b의 최대공약수`로 나눈 것과 같다.
```js
function LCM(a, b) {
    return (a * b) / GCD(a, b);
}</code></pre><hr />
<h2 id="🗂️-문제-목록-5개">🗂️ 문제 목록 (5개)</h2>
<p>분수의 덧셈🏷️
암호 해독🏷️
대문자와 소문자
인덱스 바꾸기
약수 구하기</p>