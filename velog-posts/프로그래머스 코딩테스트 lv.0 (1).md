<h3 id="올림--내림--반올림-메서드">올림 / 내림 / 반올림 메서드</h3>
<ul>
<li><code>Math.ceil()</code> 올림</li>
<li><code>Math.floor()</code> 내림</li>
<li><code>Math.round()</code> 반올림</li>
<li><code>Math.trunc()</code> 소수점 버리기
음수인 경우, <code>Math.Floor()</code>와 <code>Math.trunc()</code> 결과 차이 주의</li>
</ul>
<h3 id="문자열-안에-특정-문자열-포함-확인-메서드">문자열 안에 특정 문자열 포함 확인 메서드</h3>
<ul>
<li><code>includes()</code> // (boolean)
ex: <code>str1.includes(str2)</code>: str1 문자열에 str2 문자열 포함 여부</li>
<li><code>indexOf()</code> 특정 문자열이 처음 등장하는 위치(index). 없다면 -1</li>
<li><code>match()</code> 일치하는 문자열을 배열로 반환<pre><code class="language-js">const str1 = &quot;hello world&quot;;
const str2 = &quot;world&quot;;
</code></pre>
</li>
</ul>
<p>console.log(str1.match(str2)); // ['world']
console.log(str1.match(&quot;apple&quot;)); // null</p>
<pre><code>
### `reduce()`
`reduce((acc, cur) =&gt; acc + cur, 0)`

처음에 0부터 시작해서 배열의 요소를 하나씩 더해가며 합을 구함
- acc: 누적값 (accumulator)
- cur: 현재 요소 (current value)
- 0: 초기값


### 제곱 연산 (x의 y제곱)
- `Math.pow(x, y)`
- `x ** y`

### 제곱근 구하기
- `Math.sqrt(x)`
- `x ** 0.5`

### n이 정수인지 여부 판별
- `Number.isInteger(n)` // boolean
- `n % 1 === 0`

### `split()`: 문자열 -&gt; 배열
- `문자열.split(구분자)`
- `str.split('')` 한 글자씩 배열로 쪼갬
- ex: `'apple'.split('p')` // ['a', 'le']
'p'를 기준으로 자름 (구분자 'p'는 배열에 포함되지 않음)

### `join()`: 배열 -&gt; 문자열
- `배열.join(구분자)`
- `arr.join('')` 공백없이 합침
- ex: `['2025', '06', '04'].join('-')` // '2025-06-04'

### `replaceAll()`: 문자열 내 특정 값 변경
- `replaceAll(바꿀값, 새값)`
- `replaceAll('x', '')` // 문자열 중 x 삭제

### 스프레드 문법: 문자열 -&gt; 배열
- `[...arr]`

### `sort()` 정렬
- `arr.sort()` 문자열 정렬
- `arr.sort((a, b) =&gt; a - b)` 숫자 정렬 오름차순
- `arr.sort((a, b) =&gt; b - a)` 숫자 정렬 내림차순

### 배열 구조분해 할당
```js
const [a, b, ...rest] = [1, 2, 3, 4, 5];

console.log(a);    // 1
console.log(b);    // 2
console.log(rest); // [3, 4, 5]</code></pre><h3 id="정규식-활용">정규식 활용</h3>
<p><strong>/[aeiou]/g</strong></p>
<ul>
<li>&quot;문자열 전체에서 a, e, i, o, u 를 찾아서 바꾸자&quot;</li>
<li><code>/.../</code>: 정규식 리터럴 (패턴을 감쌈)</li>
<li><code>[aeiou]</code>:    a, e, i, o, u 중 하나에 해당하는 문자</li>
<li><code>g</code>: global — 전체 문자열에서 모두 찾음</li>
</ul>
<h3 id="숫자---문자열-변환">숫자 -&gt; 문자열 변환</h3>
<ul>
<li>String(x)</li>
<li>x.toString()</li>
</ul>
<h3 id="문자---숫자-변환">문자 -&gt; 숫자 변환</h3>
<ul>
<li>x.map(Number)</li>
</ul>
<h3 id="기타">기타</h3>
<ul>
<li><p>for문 연습</p>
<pre><code class="language-js">for (초기값; 조건식; 증감식) {
// 반복할 코드
}</code></pre>
</li>
<li><p><strong>비트연산자</strong>: 정수의 비트를 직접 다룸
성능이 중요한 저수준 연산, <strong>2의 제곱 곱셈/나눗셈 빠르게 계산 가능!</strong></p>
<ul>
<li><code>&lt;&lt;</code> 왼쪽 시프트 연산자<pre><code class="language-js">function solution(n, t) {
return n &lt;&lt; t; // 2의 t제곱
}</code></pre>
</li>
</ul>
</li>
<li><p>다양한 답변들을 보며 가독성 좋은 코드 작성에 대한 고민
: 삼항연산자? 변수 활용? 등</p>
</li>
</ul>
<h4 id="문제-목록-24개">문제 목록 (24개)</h4>
<p>나머지 구하기
두 수의 차 구하기
숫자 비교하기
나이 출력
두 수의 나눗셈
몫 구하기
두 수의 곱 구하기
두 수의 합 구하기
각도기
양꼬치
짝수의 합
문자열안에 문자열
배열의 평균값
배열 뒤집기
제곱수 판별하기
짝수 홀수 개수
특정 문자 제거하기
뒤집힌 문자열
편지
피자 나눠 먹기 (1)
세균 증식
최댓값 만들기(1)
모음 제거
자릿수 더하기</p>