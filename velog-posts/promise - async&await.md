<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/e620d0e2-72b8-4024-8944-8853f351c2b0/image.png" /></p>
<h3 id="비동기--다른-주기를-가지고-실행-현재-실행중인-코드가-종료되기-전에-다음-라인-코드-실행">비동기 : 다른 주기를 가지고 실행 (현재 실행중인 코드가 종료되기 전에 다음 라인 코드 실행)</h3>
<p>비동기적으로 실행 시 콜백 지옥 유발 가능
비동기와 상관 없는 로직이 있을 때 비동기가 끝날 때 까지 잉여 코드가 발생한다.</p>
<p><strong>해결책 : 제 3자의 개입(promise)</strong></p>
<ol>
<li>지켜보기</li>
<li>콜백 등록</li>
<li>완료 통보</li>
<li>콜백 실행</li>
</ol>
<h3 id="프로미스">프로미스</h3>
<p>콜백함수 사용으로 인한 콜백 지옥 문제나 에러처리를 해결하기 위해 탄생했다.</p>
<h3 id="작동-방식">작동 방식</h3>
<p> Promise 생성자 함수가 인수로 전달받은 콜백 함수 내부에서 비동기 처리를 수행하여 성공하면 resolve 함수를 호출하고 실패하면 reject 함수를 호출한다.</p>
<h3 id="프로미스의-상태-정보">프로미스의 상태 정보</h3>
<ul>
<li><strong>pending</strong> : 비동기 처리 수행 전 상태 / 프로미스가 생성된 직후 기본 상태</li>
<li><strong>fulfilled</strong> : 비동기 처리 성공 상태 / resolve 함수 호출</li>
<li><strong>rejected</strong> : 비동기 처리 실패 상태 / reject 함수 호출</li>
</ul>
<blockquote>
<p>프로미스의 상태는 resolve 또는 reject 함수를 호출하는 것으로 결정된다.</p>
</blockquote>
<ul>
<li><strong>settled 상태</strong> : fullfilled 또는 rejected 상태에 상관 없이 pending이 아닌 상태로 비동기 처리가 수행된 상태 -&gt; 프로미스의 후속처리 메서드(then, catch, finally)에 인수로 전달한 콜백함수가 선택적으로 호출됨 -&gt; 콜백함수에는 프로미스의 처리결과가 인수로 전달됨.</li>
</ul>
<p><strong>모든 후속 처리 메서드는 프로미스를 반환하며 비동기로 동작한다</strong></p>
<h3 id="프로미스-후속-처리-메서드">프로미스 후속 처리 메서드</h3>
<ul>
<li><p><strong>then</strong> : 두 개의 콜백 함수를 인수로 전달 받는다.</p>
<ul>
<li>첫 번째 콜백 함수는 프로미스가 resolve 함수가 호출된 상태가 되면 호출된다. 이때 콜백 함수는 프로미스의 비동기 처리 결과를 인수로 전달받는다. (성공 처리 콜백 함수)</li>
<li>두 번째 콜백 함수는 프로미스가 reject 함수가 호출된 상태가 되면 호출된다. 이때 콜백 함수는 프로미스의 에러를 인수로 전달받는다. (실패 처리 콜백 함수)<blockquote>
<p>then 메서드는 언제나 프로미스를 반환한다.</p>
</blockquote>
</li>
</ul>
</li>
<li><p><strong>catch</strong> : 한 개의 콜백 함수를 인수로 전달 받는다.</p>
<ul>
<li>catch 메서드의 콜백 함수는 프로미스가 rejected 상태인 경우만 호출된다.</li>
<li>then 메서드와 동일하게 동작한다.</li>
</ul>
</li>
<li><p><strong>finally</strong> : 한 개의 콜백 함수를 인수로 전달받는다.</p>
<ul>
<li>프로미스의 성공 실패와 상관 없이 무조건 한 번 호출된다.</li>
<li>프로미스의 상태와 상관없이 공통적으로 수행해야 할 처리 내용이 있을 때 사용된다.</li>
</ul>
</li>
</ul>
<h3 id="프로미스-체이닝--후속-처리-메서드를-연속으로-호출">프로미스 체이닝 : 후속 처리 메서드를 연속으로 호출</h3>
<p>후속처리 메서드의 콜백 함수는 프로미스의 비동기 처리 상태가 변경되면 선택적으로 호출된다. (콜백 함수가 반환한 프로미스에 따라)</p>
<pre><code class="language-javascript">const myPromise = new Promise((resolve, reject) =&gt; {
  setTimeout(() =&gt; {
    resolve("foo");
  }, 300);
});

myPromise
  .then(handleFulfilledA)
  .then(handleFulfilledB)
  .then(handleFulfilledC)
  .catch(handleRejectedAny);
</code></pre>
<p>화살표 함수를 사용한 프로미스 체인 구현</p>
<pre><code class="language-javascript">myPromise
  .then((value) =&gt; `${value} and bar`)
  .then((value) =&gt; `${value} and bar again`)
  .then((value) =&gt; `${value} and again`)
  .then((value) =&gt; `${value} and again`)
  .then((value) =&gt; {
    console.log(value);
  })
  .catch((err) =&gt; {
    console.error(err);
  });</code></pre>
<h3 id="프로미스-정적-메서드">프로미스 정적 메서드</h3>
<ul>
<li><strong>resolve</strong> : 인수로 전달받은 값을 resolve하는 프로미스 생성</li>
<li><strong>rejected</strong> : 인수로 전달받은 값을 rejected하는 프로미스 생성</li>
<li><strong>all</strong> : 여러 개의 비동기 처리를 모두 병렬 처리할 때 사용</li>
<li><strong>race</strong> : 프로미스를 요소로 갖는 배열 등의 이터러블을 인수로 전달 받음<ul>
<li>모든 프로미스가 fullfilled 상태가 될 때까지 기다리는 것이 아니라 가장 먼저 fullfilled 상태가 된 프로미스의 처리 결과를 resolve하는 새로운 프로미스 반환</li>
<li>프로미스가 rejected 상태가 되면 all 메소드와 동일하게 처리</li>
</ul>
</li>
<li><strong>allSettled</strong> : 프로미스를 요소로 갖는 배열 등의 이터러블을 인수로 전달 받음<ul>
<li>전달받은 프로미스가 모두 settled 상태가 되면 처리결과를 배열로 반환</li>
</ul>
</li>
<li>allSettled가 반환한 배열에는 인수로 전달받은 모든 프로미스들의 처리 결과가 담겨 있다.<ul>
<li>프로미스가 fullfilled 상태인 경우 비동기 처리 상태를 나타내는 status 프로퍼티와 처리 결과를 나타내는 value 프로퍼티를 가짐</li>
<li>프로미스가 rejected 상태인 경우 비동기 처리 상태를 나타내는 status 프로퍼티와 에러를 나타내는 reason 프로퍼티를 가짐</li>
</ul>
</li>
</ul>