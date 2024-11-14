<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/64145f52-f1ac-484c-baa1-25db357aed55/image.png" /></p>
<p>프로미스는 비동기 처리를 위한 또 다른 패턴으로 전통적인 콜백 패턴이 가진 단점을 보완하며 비동기 처리 시점을 명확하게 표현할 수 있는 장점이 있다.</p>
<p><strong>비동기 함수는 비동기 처리 결과를 외부에 반환할 수 없고 상위 스코프의 변수에 할당할 수도 없다.
따라서 비동기 함수의 처리결과에 대한 후속 처리는 비동기 함수 내부에서 수행해야 한다.</strong></p>
<p>이때 콜백 함수를 전달하여 비동기 함수를 사용한다.</p>
<h3 id="비동기-처리를-위한-콜백-패턴의-단점">비동기 처리를 위한 콜백 패턴의 단점</h3>
<ul>
<li><p>콜백 헬 : 콜백 함수를 통해 비동기 처리 결과에 대한 후속 처리를 수행하는 비동기 함수가 비동기 처리 결과를 가지고 또다시 비동기 함수를 호출해야 한다면 콜백 함수 호출이 중첩되어 복잡도가 높아지는 현상</p>
<ul>
<li>비동기 함수를 호출하면 함수 내부의 비동기로 동작하는 코드가 완료되지 않았다 해도 기다리지 않고 즉시 종료된다. 비동기 함수 내부의 비동기로 동작하는 코드에서 처리 결과를 외부로 반환하거나 상위 스코프의 변수에 할당하면 기대한대로 동작하지 않는다.</li>
</ul>
</li>
<li><p>에러 처리의 한계</p>
</li>
</ul>
<h3 id="프로미스의-생성">프로미스의 생성</h3>
<p>Promise 생성자 함수를 new 연산자와 함께 호출하면 프로미스를 생성한다.</p>
<p>Promise 생성자 함수는 비동기 처리를 수행할 콜백 함수를 인수로 전달받아 resolve와 reject 함수를 인수로 전달받는다.</p>
<p>비동기 처리가 성공하면 resolve 함수를 호출하고 비동기 처리가 실패하면 reject 함수를 호출한다.</p>
<h3 id="프로미스의-3가지-상태-정보">프로미스의 3가지 상태 정보</h3>
<ul>
<li>Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태 | 프로미스 생성 직후 상태<pre><code class="language-javascript">new Promise();
</code></pre>
</li>
</ul>
<p>new Promise(function(resolve, reject) {
  // ...
});</p>
<pre><code>- Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태 | resolve 함수 호출
```javascript
new Promise(function(resolve, reject) {
  resolve();
});

function getData() {
  return new Promise(function(resolve, reject) {
    var data = 100;
    resolve(data);
  });
}

// resolve()의 결과 값 data를 resolvedData로 받음
getData().then(function(resolvedData) {
  console.log(resolvedData); // 100
});
</code></pre><ul>
<li>Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태 | reject 함수 호출<pre><code class="language-javascript">new Promise(function(resolve, reject) {
reject();
});
</code></pre>
</li>
</ul>
<p>function getData() {
  return new Promise(function(resolve, reject) {
    reject(new Error("Request is failed"));
  });
}</p>
<p>// reject()의 결과 값 Error를 err에 받음
getData().then().catch(function(err) {
  console.log(err); // Error: Request is failed
});</p>
<pre><code>
![](https://velog.velcdn.com/images/se0kcess/post/4945c43e-e507-464c-ba80-4cb2c6f369f2/image.png)
프로미스 처리 흐름 - MDN

### 프로미스의 상태 변경
- 비동기 처리 성공 : resolve 함수를 호출해 프로미스를 fullfilled 상태로 변경
- 비동기 처리 실패 : reject 함수를 호출해 프로미스를 rejected 상태로 변경

![](https://velog.velcdn.com/images/se0kcess/post/8534e67d-5c2d-4568-b398-557afa90d013/image.png)

settled 상태 : fullfilled 또는 rejected 상태 | pending이 아닌 상태, 비동기 처리가 수행된 상태

settled 상태가 되면 다른 상태로 변화할 수 없다.

---

비동기 처리가 성공하면 프로미스는 pending 상태에서 fullfilled 상태로 변화한다. 그리고 비동기 처리 결과 값인 1을 갖는다.


비동기 처리가 실패하면 프로미스는 pending 상태에서 rejected 상태로 변화한다. 그리고 비동기 처리 결과 값인 Error 객체를 값으로 갖는다.

&gt;프로미스는 비동기 처리 상태와 처리 결과를 관리하는 객체다

### 프로미스의 후속 처리 메서드
프로미스의 비동기 처리 상태가 변화하면 이에 따른 후속 처리를 해야한다.

프로미스의 비동기 처리 상태가 변화하면 후속 처리 메서드에 인수로 전달할 콜백 함수가 선택적으로 호출된다.

### Promise.prototype.then
then 메서드는 두 개의 콜백 함수를 인수로 전달받는다.
 - 첫 번째 콜백 함수는 프로미스가 fullfilled 상태가 되면 호출된다. 이때 콜백 함수는 프로미스의 비동기 처리 결과를 인수로 전달받는다
 - 두 번째 콜백 함수는 프로미스가 reject 상태가 되면 호출된다. 이때 콜백 함수는 프로미스의 에러를 인수로 전달받는다

첫 번째 콜백 함수는 비동기 처리가 성공했을 때 호출되는 성공 처리 콜백 함수이며, 두 번째 콜백 함수는 비동기 처리가 실패했을 때 호출되는 실패 처리 콜백 함수다.

then메서드는 언제나 프로미스를 반환한다. 만약 then 메서드의 콜백 함수가 프로미스를 반환하면 그 프로미스를 그대로 반환하고 콜백 함수가 프로미스가 아닌 값을 반환하면 그 값을 암묵적으로 resolve 또는 reject하여 프로미스를 생성해 반환한다.

### Promise.prototype.catch
catch 메서드는 한 개의 콜백 함수를 인수로 전달 받는다. catch 메서드의 콜백 함수는 프로미스가 rejected 상태인 경우만 호출된다.

catch 메서드는 then과 동일하게 동작한다. 따라서 then 메서드와 마찬가지로 언제나 프로미스를 반환한다.

### Promise.prototype.finally
finally 메서드는 한 개의 콜백 함수를 인수로 전달받는다. finally 메서드의 콜백 함수는 프로미스의 성공 또는 실패와 상관없이 무조건 한 번 호출된다. finally 메서드는 프로미스의 상태와 상관없이 공통적으로 수행해야 할 처리 내용이 있을 때 유용하다. 언제나 프로미스를 반환한다.

### 프로미스의 에러 처리
then 메서드의 두 번째 콜백 함수로 처리
![](https://velog.velcdn.com/images/se0kcess/post/1d447791-fd2b-4ae6-9c96-d31d4016f800/image.png)


catch 메서드를 사용해 처리
![](https://velog.velcdn.com/images/se0kcess/post/932496ca-6a7a-49fd-aa0e-2cae3511e97f/image.png)


catch 메서드를 모든 then 메서드를 호출한 이후에 호출하면 비동기 처리에서 발생한 에러 뿐만 아니라 then 메서드 내부에서 발생한 에러까지 모두 캐치 가능하다.

then 메서드에 두 번째 콜백 함수를 전달하는 것보다 catch 메서드를 사용하는 것이 가독성이 좋고 명확하다. 따라서 에러 처리는 then 메서드에서 하지 말고 catch 메서드에서 하는 것을 권장한다.

### 프로미스 체이닝
then, catch, finally 후속 처리 메서드를 연속적으로 호출 가능하다.

```javascript
function getData() {
  return new Promise({
    // ...
  });
}

// then() 으로 여러 개의 프로미스를 연결한 형식
getData()
  .then(function(data) {
    // ...
  })
  .then(function() {
    // ...
  })
  .then(function() {
    // ...
  });</code></pre><p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/8b9b8a83-d4ef-493b-b6bd-979cee517436/image.png" /></p>
<p>then, catch finally 후속 처리 메서드는 콜백 함수가 반환한 프로미스를 반환한다. 만약 후속 처리 메서드의 콜백 함수가 프로미스가 아닌 값을 반환하더라도 그 값을 암묵적으로 resolve 또는 reject하여 프로미스를 생성해 반환한다.</p>
<p>프로미스는 프로미스 체이닝을 통해 비동기 처리 결과를 전달받아 후속 처리를 하므로 비동기 처리를 위한 콜백 패턴에서 발생하던 콜백 헬이 발생하지 않는다. 다만 프로미스도 콜백 패턴을 사용하므로 콜백 함수를 사용하지 않는 것은 아니다</p>
<h3 id="프로미스의-정적-메서드">프로미스의 정적 메서드</h3>
<p>Promise는 주로 생성자 함수로 사용되지만 함수도 객체이므로 메서드를 가질 수 있다.</p>
<h3 id="promisepromiseresolve--promisereject">PromisePromise.resolve / Promise.reject</h3>
<p>이미 존재하는 값을 래핑하여 프로미스를 생성하기 위해 사용한다.</p>
<ul>
<li>Promise.resolve 메서드는 인수로 전달받은 값을 resolve하는 프로미스를 생성한다.</li>
<li>Promise.reject 메서드는 인수로 전달받은 값을 reject하는 프로미스를 생성한다.</li>
</ul>
<h3 id="promiseall">Promise.all</h3>
<p>여러 개의 비동기 처리를 모두 병렬 처리할 때 사용한다.</p>
<h3 id="promiserace">Promise.race</h3>
<ul>
<li>Promise.all 메서드와 동일하게 프로미스를 요소로 갖는 배열 등의 이터러블을 인수로 전달받는다.</li>
<li>Promise.all 처럼 모든 프로미스가 fulfilled 상태가 되는 것을 기다리는 것이 아니라 가장 먼저</li>
<li>fulfilled 상태가 된 프로미스의 처리 결과를 resolve하는 새로운 프로미스를 반환한다.</li>
</ul>
<h3 id="promiseallsettled">Promise.allSettled</h3>
<ul>
<li>전달받은 프로미스가 모두 settled 상태가 되면 처리 결과를 배열로 반환한다.</li>
<li>Promise.allSettled 메서드가 반환한 배열에는 fulfilled 또는 rejected 상태와는 상관없이</li>
<li>Promise.allSettled 메서드가 인수로 전달받은 모든 프로미스들의 처리 결과가 모두 담겨 있다.</li>
</ul>
<h3 id="마이크로태스크-큐">마이크로태스크 큐</h3>
<p>콜백 함수나 이벤트 핸들러를 일시 저장한다는 점에서 태스크 큐와 동일하지만 마이크로태스크 큐는 태스크 큐보다 우선순위가 높다.</p>
<h3 id="fetch">fetch</h3>
<p>fetch 함수는 XMLHttpRequest 객체와 마찬가지로 HTTP 요청 전송 기능을 제공하는 클라이언트 사이드 Web API다.</p>
<ul>
<li><p>XMLHttpRequest 객체보다 사용법이 간단하고 프로미스를 지원하기 때문에 비동기 처리를 위한 콜백 패턴의 단점에서 자유롭다.</p>
</li>
<li><p>HTTP 요청을 전송할 URL과 HTTP 요청 메서드, HTTP 요청 헤더, 페이로드 등을 설정한 객체를 전달한다.</p>
</li>
<li><p>HTTP 응답을 나타내는 Response 객체를 래핑한 Promise 객체를 반환한다.</p>
</li>
</ul>
<p>따라서 fetch 함수를 사용할 때는 fetch 함수가 반환한 프로미스가 resolve한 불리언 타입의 ok 상태를 확인해 명시적으로 에러를 처리해야 한다.</p>