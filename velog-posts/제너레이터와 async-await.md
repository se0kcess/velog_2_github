<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/cff1ad27-7cfc-4b1d-9b6f-fbf0a141486f/image.png" /></p>
<h3 id="제너레이터">제너레이터</h3>
<p>코드 블록의 실행을 일시 중지했다가 필요한 시점에 재개할 수 있는 특수한 함수</p>
<h3 id="제너레이터와-일반-함수의-차이">제너레이터와 일반 함수의 차이</h3>
<ul>
<li>제너레이터 함수는 함수 호출자에게 함수 실행의 제어권을 양도할 수 있다.</li>
<li>제너레이터 함수는 함수 호출자와 함수의 상태를 주고받을 수 있다.</li>
<li>제너레이터 함수를 호출하면 제너레이터 객체를 반환한다.</li>
</ul>
<h3 id="제너레이터-함수의-정의">제너레이터 함수의 정의</h3>
<p>제너레이터 함수는 function 키워드로 선언한다. 그리고 하나 이상의 yeild 표현식을 포함한다. 이것을 제외하면 일반 함수를 정의하는 방법과 같다.</p>
<h3 id="제너레이터-객체">제너레이터 객체</h3>
<p>제너레이터 함수를 호출하면 일반 함수처럼 함수 코드 블록을 실행하는 것이 아니라 제너레이터 객체를 생성해 반환한다. 제너레이터 함수가 반환한 제너레이터 객체는 이터러블 이면서 동시에 이터레이터다.</p>
<h3 id="제너레이터-객체의-메서드">제너레이터 객체의 메서드</h3>
<ul>
<li><p>throw : 인수로 전달받은 에러를 발생시키고 undefined를 value 프로퍼티 값으로, true를 done 프로퍼티 값으로 갖는 이터레이터 리절트 객체를 반환한다.</p>
</li>
<li><p>return : 인수로 전달받은 값을 value 프로퍼티 값으로, true를 done 프로퍼티 값으로 갖는 이터레이터 리절트 객체를 반환한다.</p>
</li>
<li><p>throw : 인수로 전달받은 에러를 발생시키고 undefined를 value 프로퍼티 값으로, true를 done 프로퍼티 값으로 갖는 이터레이터 리절트 객체를 반환한다.</p>
</li>
</ul>
<h3 id="제너레이터의-일시-중지와-재개">제너레이터의 일시 중지와 재개</h3>
<ul>
<li><p>yield : 제너레이터 함수의 실행을 일시 중지시키거나 yield 키워드 뒤에 오는 표현식의 평가 결과를 제너레이터 함수 호출자에게 반환한다.</p>
</li>
<li><p>next : yield 표현식까지 실행되고 일시중지된다. 이때 함수의 제어권이 호출자로 양도된다. | value, done 프로퍼티를 갖는 이터레이터 리절트 객체를 반환한다.</p>
</li>
</ul>
<p>next 메서드가 반환한 이터레이터 리절트 객체의 value 프로퍼티에는 yield 표현식에서 yield 된 값이 할당되고 done 프로퍼티에는 제너레이터 함수가 끝까지 실행되었는지를 나타내는 불리언 값이 할당된다.</p>
<p>이터레이터의 next 메서드와 달리 제너레이터 객체의 next 메서드에는 인수를 전달할 수 있다. 제너레이터 객체의 next 메서드에 전달한 인수는 제너레이터 함수의 yield 표현식을 할당받는 변수에 할당된다.</p>
<h3 id="제너레이터의-활용">제너레이터의 활용</h3>
<ul>
<li>이터러블의 구현</li>
<li>비동기 처리</li>
</ul>
<h2 id="asyncawait">async/await</h2>
<p>제너레이터보다 간단하고 가독성 좋게 비동기 처리를 동기 처리처럼 동작하도록 구현할 수 있는 async/await가 도입되었다.</p>
<ul>
<li>async/await는 프로미스를 기반으로 동작한다.</li>
<li>async/await를 사용하면 후속 처리 메서드 없이 마치 동기 처리처럼 프로미스를 사용할 수 있다.</li>
</ul>
<h3 id="async-함수">async 함수</h3>
<ul>
<li>await 키워드는 반드시 async 함수 내부에서 사용해야 한다.</li>
<li>async 함수는 async 키워드를 사용해 정의하며 언제나 프로미스를 반환한다.</li>
<li>async 함수가 명시적으로 프로미스를 반환하지 않더라도 async 함수는 암묵적으로 반환값을 resolve하는 프로미스를 반환한다.</li>
</ul>
<h3 id="await-키워드">await 키워드</h3>
<ul>
<li>await 키워드는 프로미스가 settled 상태가 될 때까지 대기하다가 settled 상태가 되면 프로미스가 resolve한 처리 결과를 반환한다.</li>
<li>await 키워드는 반드시 프로미스 앞에서 사용해야 한다.</li>
</ul>
<h3 id="에러-처리">에러 처리</h3>
<p>try...catch 문을 사용해서 에러처리가 가능하다.</p>
<p>async 함수 내에서 catch 문을 사용해서 에러 처리를 하지 않으면 async 함수는 발생한 에러를 reject 하는 프로미스를 반환한다.</p>
<h3 id="async--await-기본-문법">async &amp; await 기본 문법</h3>
<pre><code class="language-js">async function 함수명() {
  await 비동기_처리_메서드_명();
}</code></pre>
<p>함수의 앞에 async 라는 예약어를 붙인다. 그러고 나서 함수의 내부 로직 중 HTTP 통신을 하는 비동기 처리 코드 앞에 await를 붙인다. 주의해야 할 점은 비동기 처리 메서드가 꼭 프로미스 객체를 반환해야 await가 의도한 대로 동작한다.</p>
<p>일반적으로 await의 대상이 되는 비동기 처리 코드는 Axios 등 프로미스를 반환하는 API 호출 함수이다.</p>