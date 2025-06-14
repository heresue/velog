<h2 id="🔎-주요-문제-풀이">🔎 주요 문제 풀이</h2>
<h3 id="개미-군단">개미 군단</h3>
<blockquote>
<p>개미 군단이 사냥을 나가려고 합니다. 개미군단은 사냥감의 체력에 딱 맞는 병력을 데리고 나가려고 합니다. 장군개미는 5의 공격력을, 병정개미는 3의 공격력을 일개미는 1의 공격력을 가지고 있습니다. 예를 들어 체력 23의 여치를 사냥하려고 할 때, 일개미 23마리를 데리고 가도 되지만, 장군개미 네 마리와 병정개미 한 마리를 데리고 간다면 더 적은 병력으로 사냥할 수 있습니다. 사냥감의 체력 hp가 매개변수로 주어질 때, 사냥감의 체력에 딱 맞게 최소한의 병력을 구성하려면 몇 마리의 개미가 필요한지를 return하도록 solution 함수를 완성해주세요.</p>
</blockquote>
<h4 id="🔷-풀이">🔷 풀이</h4>
<p><strong>- 1번째 풀이 (반복문)</strong></p>
<pre><code class="language-js">function solution(hp) {
    const antStr = [5, 3, 1]
    let count = 0

    antStr.forEach((x) =&gt; {
        count += Math.floor(hp / x)
        hp %= x
    })

    return count
}</code></pre>
<p><strong>- 2번째 풀이 (단순 계산)</strong></p>
<pre><code class="language-js">function solution(hp) {
    const ant1 = 5
    const ant2 = 3
    const ant3 = 1

    let count = 0;

    count += Math.floor(hp / ant1)
    hp %= ant1

    count += Math.floor(hp / ant2)
    hp %= ant2

    count += Math.floor(hp / ant3)

    return count
}</code></pre>
<p><strong>- 3번째 풀이 (단순 계산)</strong></p>
<pre><code class="language-js">function solution(hp) {
    return Math.floor(hp / 5) 
        + Math.floor((hp % 5) / 3) 
        + Math.floor(hp % 5 % 3)
}</code></pre>
<p>유지보수를 생각하면 1번째 풀이가 좋아보이지만, 숫자가 바뀔 가능성이 없거나 코딩테스트같은 경우는 단순 계산식으로 해도 괜찮을 것 같다. 3번의 계산 안에 끝나기 때문에 반복문으로 작성하는 것이 오버헤드가 될 가능성이 더 크기 때문에..!
(하지만 난 1번 코드가 제일 좋아..)</p>
<hr />
<h3 id="가위-바위-보">가위 바위 보</h3>
<blockquote>
<p>가위는 2 바위는 0 보는 5로 표현합니다. 가위 바위 보를 내는 순서대로 나타낸 문자열 rsp가 매개변수로 주어질 때, rsp에 저장된 가위 바위 보를 모두 이기는 경우를 순서대로 나타낸 문자열을 return하도록 solution 함수를 완성해보세요.</p>
</blockquote>
<h4 id="🔷-풀이-1">🔷 풀이</h4>
<p><strong>- 1번째 풀이 (for문)</strong></p>
<pre><code class="language-js">function solution(rsp) {
    const rock = &quot;0&quot;
    const scissors = &quot;2&quot;
    const paper = &quot;5&quot;

    const rsp_list = rsp.split('')
    let answer = &quot;&quot;

   for(let i = 0; i &lt; rsp_list.length; i++) {
        answer += (rsp_list[i] == rock) ? paper
        : rsp_list[i] == scissors ? rock
        : scissors
    }
    return answer
}</code></pre>
<ul>
<li>중첩 삼항은 되도록 피하고, map 등을 활용하자</li>
</ul>
<p><strong>- 2번째 풀이 (객체)</strong></p>
<pre><code class="language-js">function solution(rsp) {
    const win_map = {
        &quot;2&quot;: &quot;0&quot;,
        &quot;0&quot;: &quot;5&quot;,
        &quot;5&quot;: &quot;2&quot;
    }

    return rsp.split('').map(x =&gt; win_map[x]).join('')
}</code></pre>
<ul>
<li>객체를 활용하니, 간단하면서도 유지보수하기 좋은 코드로 구현 가능했다.</li>
<li><em>각각 대응되는 값이 있다면 객체 활용하기!*</em></li>
</ul>
<hr />
<h2 id="🗂️-문제-목록-3개">🗂️ 문제 목록 (3개)</h2>
<p>개미 군단🏷️
가위 바위 보🏷️
옹알이 (1)</p>