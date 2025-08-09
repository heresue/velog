<p><em>(본 글은 SSR 환경에서의 TanStack Query를 주제로 하였기에, Next.js, SSR/CSR, TanStack Query 등에 대한 자세한 내용은 별도 포스팅에서 다루도록 하겠습니다.)</em></p>
<hr />
<h2 id="tanstack-queryreact-query-등장-배경">TanStack Query(React Query) 등장 배경</h2>
<blockquote>
<p><em>&quot;TanStack Query는 서버 상태 관리를 위한 단연코 최고의 라이브러리이다.
(TanStack Query is hands down one of the best libraries for managing server state.)&quot;</em>
― TanStack Query <a href="https://tanstack.com/query/latest/docs/framework/react/overview#motivation">공식문서</a></p>
</blockquote>
<p>React에서 상태 관리를 하는 이유는 효율적이고 일관된 방식으로 상태를 다루기 위해서이다.
기존 전역 상태 관리 라이브러리(Redux, Zustand 등)는 클라이언트 상태(Client State)를 관리하기에는 유용하지만, 서버 상태(Server State)를 관리할 때에는 불필요하게 복잡한 로직과 보일러플레이트가 발생하게 되었다.</p>
<p>서버 상태는 다음과 같은 특성을 가진다.</p>
<ul>
<li>서버에 존재하며 비동기적으로 가져와야 함</li>
<li>항상 최신성을 보장해야 함</li>
<li>클라이언트에서 직접 수정이 불가함</li>
<li>캐싱, 동기화, 오류 처리 등 부가 로직이 필요</li>
</ul>
<p>이러한 특성 때문에 데이터 fetching, 캐싱, 무효화, 에러/로딩 관리, 포커스 시 재검증 등의 기능을 직접 구현해야 하는 불편함이 있었다. TanStack Query는 이러한 문제를 해결하고, 선언적인 프로그래밍으로 서버 상태를 효율적으로 관리할 수 있도록 도와주는 비동기 상태 관리 라이브러리이다.</p>
<h2 id="ssr-server-side-rendering과-nextjs의-app-router-도입">SSR (Server Side Rendering)과 Next.js의 App Router 도입</h2>
<p>React는 CSR(Client Side Rendering) 방식의 SPA(Single Page Application)으로, 초기 HTML은 비어 있고 JavaScript를 로드하여 모든 페이지를 렌더링한다. 이로 인해 첫 화면이 느리게 나타나는 문제가 발생할 수 있다.
이를 해결할 수 있는 방식이 바로 SSR이다. SSR은 서버 사이드 렌더링, 말 그대로 서버에서 미리 정적인 HTML을 생성하여 렌더링하는 방식으로, 초기 화면을 빠르게 보여줌으로써 사용자 경험(UX)을 해치지 않고 SEO에도 유리하다.
Next.js는 React에서 SSR, SSG, CSR 등 다양한 렌더링 전략을 제공하는 프레임워크로 등장하였으나, 기존 Page Router 기반에서는 SSR을 사용하려면 별도의 설정을 하는 등 설정이 복잡하고 유연성이 떨어지는 측면이 있었다.
이후 React 18에서 RSC(React Server Component)라는 서버 컴포넌트 기술이 등장하였고, Next.js 13버전부터 RSC를 포함한 React 18의 새로운 기능들을 활용하기 위해 App Router라는 새로운 라우팅 방식를 도입하게 되었다. App Router는 기본적으로 SSR을 지원한다. 모든 컴포넌트를 서버 컴포넌트(RSC)로 사용하며, 서버 액션(Server Actions)을 통해 서버에서 직접 비동기 로직과 데이터 변경까지 처리할 수 있게 되었다.</p>
<h2 id="tanstack-query를-ssr-환경에서-써야하는-이유">TanStack Query를 SSR 환경에서 써야하는 이유</h2>
<p>Next.js의 App Router에 기본적으로 내장된 기능들은 다음 표와 같다.</p>
<h4 id="nextjs의-내장-기능-app-router">Next.js의 내장 기능 (App Router)</h4>
<table>
<thead>
<tr>
<th>기능</th>
<th>Next.js (App Router)</th>
</tr>
</thead>
<tbody><tr>
<td>초기 데이터 로딩</td>
<td>Server Component에서 <code>fetch</code></td>
</tr>
<tr>
<td>캐싱</td>
<td><code>fetch</code> 옵션(<code>force-cache</code>, <code>revalidate</code>, <code>tags</code>)</td>
</tr>
<tr>
<td>데이터 갱신</td>
<td><code>revalidatePath</code>, <code>revalidateTag</code></td>
</tr>
<tr>
<td>SSG/ISR</td>
<td><code>generateStaticParams</code>, <code>revalidate</code></td>
</tr>
<tr>
<td>스트리밍 렌더링</td>
<td><code>&lt;Suspense&gt;</code>, <code>loading.tsx</code></td>
</tr>
<tr>
<td>서버 액션</td>
<td>서버에서 직접 mutation 처리</td>
</tr>
<tr>
<td>이 기능들을 보면, 충분히 기본 기능으로도 서버 상태를 다룰 수 있어 보인다. 그렇다면 TanStack Query를 SSR 환경에서 써야하는 이유는 무엇일까?</td>
<td></td>
</tr>
</tbody></table>
<p>SSR 방식은 초기에 화면을 빠르게 렌더링하는 것에는 강점이 있지만, 이후 클라이언트에서 데이터가 계속 변하는 상황이나 상호작용이 많은 경우 등과 같이 사용자의 흐름까지 제어하기에는 한계가 있다. TanStack Query는 이러한 사용자 인터랙션을 모두 포함한 전반적인 데이터들을 효율적으로 관리하도록 돕는다. 특히 다음과 같은 경우를 예로 들 수 있다.</p>
<ul>
<li>대시보드, 피드 등 데이터 변경이 잦은 UI를 제공하는 경우</li>
<li>중복 요청 방지 및 불필요한 로딩 제거</li>
<li>자동 리패칭, 에러 처리, 포커스 시 갱신 등</li>
<li>낙관적 업데이트, 무한스크롤 구현 등</li>
</ul>
<p>Next.js의 기본 기능만으로도 구현은 가능하지만 매번 로직을 반복해야 하고 특히 캐싱이나 중복 요청 방지 등과 같은 로직은 직접 관리해야 하며, 유지보수가 어려워지는 등의 불편함이 있다. 반면, TanStack Query에서는 이러한 기능들을 기본적으로 제공하고 있다.</p>
<h4 id="nextjs와-tanstack-query의-기능-비교">Next.js와 TanStack Query의 기능 비교</h4>
<table>
<thead>
<tr>
<th>기능</th>
<th>Next.js(App Router)</th>
<th>TanStack Query</th>
</tr>
</thead>
<tbody><tr>
<td>캐싱</td>
<td>fetch 캐시 (전역적)</td>
<td>쿼리 키 기반 세분화 캐싱</td>
</tr>
<tr>
<td>데이터 무효화</td>
<td><code>revalidatePath</code>, <code>revalidateTag</code></td>
<td><code>invalidateQueries</code> (세분화, 부분 무효화)</td>
</tr>
<tr>
<td>포커스/네트워크 복귀 시 갱신</td>
<td>직접 구현 필요</td>
<td>기본 제공</td>
</tr>
<tr>
<td>무한 스크롤</td>
<td>직접 구현 필요</td>
<td><code>useInfiniteQuery</code></td>
</tr>
<tr>
<td>낙관적 업데이트</td>
<td>직접 구현 필요</td>
<td>기본 제공</td>
</tr>
<tr>
<td>오프라인/멀티탭 동기화</td>
<td>직접 구현 필요</td>
<td>기본 제공</td>
</tr>
</tbody></table>
<h2 id="tanstack-query를-언제-사용해야-할까">TanStack Query를 언제 사용해야 할까?</h2>
<p>실제 프로젝트를 진행하게 되면, 막상 라이브러리를 사용함에 있어 많은 고민을 하게 된다. TanStack Query 역시 적절하게 사용한다면 굉장히 효율적인 라이브러리로써 기능하게 되지만, 그렇지 않은 경우 &quot;굳이?&quot;라는 의문을 남길 수 있다. 위 내용을 정리해보면 TanStack Query는 서버 상태 관리, 특히 클라이언트 단에서 데이터를 재사용하고 관리할 때 효율적인 상태 관리 라이브러리이다. 이와 같은 특성에 따라, 아래와 같은 체크리스트로 프로젝트에 적절한 지를 우선적으로 판단해볼 수 있을 것 같다.</p>
<ul>
<li>데이터가 자주 변경되고, 이를 화면에 즉시 반영해야 하는가?</li>
<li>페이지 내에서 상호작용이 많고 데이터 갱신이 자주 일어나야 하는가?</li>
<li>포커스/네트워크 복구 시 자동 갱신이 필요한가?</li>
<li>무한 스크롤, 페이지네이션이 필요한가?</li>
<li>다수의 API 요청 캐싱과 동기화가 필요한가?</li>
</ul>
<p>위와 같은 경우가 아닌, 읽기 전용이거나 변경 빈도가 낮은 데이터를 주로 사용하는 경우라면 기본 기능만으로도 충분하다.</p>
<h2 id="comment">Comment</h2>
<p>Next.js(App Router) 기반의 프로젝트에 처음으로 TanStack Query를 도입하고자 했을 때는 TanStack Query가 특히 Next.js 환경에서 어떤 강점을 보일 수 있는지에 대한 고민이 부족했던 것 같다. SSR 환경에서, 서버 상태를 관리하는 데에 특화된 TanStack Query를 좀 더 전략적으로 사용한다면 클라이언트 인터랙션과 관련한 다양한 기능들을 좀 더 간단하게 구현할 수 있을 것 같다는 생각이 들었다. 다음으로는 TanStack Query에 대해 좀 더 딥다이브하고 프로젝트에 적용해보면서, 이전에 사용했던 프로젝트와도 비교하는 등의 과정을 통해 TanStack Query를 더 깊게 이해하는 시간을 가져봐야겠다.</p>