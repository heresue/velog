<h2 id="⭐-요구사항">⭐ 요구사항</h2>
<blockquote>
<p>Keyboard 입력을 받아 애니메이션 효과와 Drum 소리가 출력되는 drum kit 구현하기</p>
</blockquote>
<h3 id="--작성-코드">- 작성 코드</h3>
<pre><code class="language-js">document.addEventListener(&quot;keydown&quot;, (e) =&gt; {
  const keyCode = e.key.toLowerCase();
  const $key = document.querySelector(`div[data-key=&quot;${keyCode}&quot;]`);
  const $audio = document.querySelector(`audio[data-key=&quot;${keyCode}&quot;]`);

  // 방어 코드: 요소가 없을 경우 에러 방지
  if (!$key) return;

  $key.classList.add(&quot;key-press&quot;);

  if ($audio) {
    $audio.currentTime = 0; // 재생 위치를 처음으로
    $audio.play();
  }

  setTimeout(() =&gt; {
    $key.classList.remove(&quot;key-press&quot;);
  }, 150);
});
</code></pre>
<ul>
<li>key의 값을 <code>id</code>가 아닌 <code>data-*</code> 속성으로 설정 (<code>data-key</code>)</li>
<li><code>const keyCode = e.key.toLowerCase();</code>: 대소문자 문제 방지</li>
</ul>
<hr />
<h2 id="📝-메모">📝 메모</h2>
<h3 id="css-세로-가운데-정렬">CSS 세로 가운데 정렬</h3>
<h4 id="--flexbox">- Flexbox</h4>
<pre><code class="language-js">.container {
  display: flex;
  justify-content: center; /* 가로 가운데 */
  align-items: center;     /* 세로 가운데 */
}</code></pre>
<h4 id="--grid">- Grid</h4>
<pre><code class="language-js">.container {
  display: grid;
  place-items: center;
}</code></pre>
<h4 id="--position--transform-방식">- position + transform 방식</h4>
<pre><code class="language-js">.container {
  position: relative;
}

.item {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}</code></pre>
<ul>
<li>구버전 브라우저 호환</li>
<li>크기가 불명확한 경우에도 안전하게 사용 가능</li>
<li>부모 요소의 <code>position: relative</code> 필요</li>
</ul>
<h4 id="--line-height-text">- line-height (text)</h4>
<pre><code class="language-js">.container {
  height: 200px;
  line-height: 200px;
  text-align: center;
}</code></pre>
<ul>
<li>단일 텍스트 요소에서 빠르게 적용 가능</li>
</ul>