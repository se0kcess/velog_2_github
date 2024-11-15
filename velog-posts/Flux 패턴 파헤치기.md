<blockquote>
<p>리액트를 공부하고 프로젝트를 진행하면서, 리액트에 사용되는 디자인 패턴인 Flux 패턴에 대해 간단한 동작 원리만 알고 왜 react에 사용되는지, 다른 디자인 패턴인 mvc 패턴과의 차이점은 무엇인지는 알지 못했다.</p>
</blockquote>
<p>그래서 이번 기회에 Flux 패턴에 대해 파헤쳐보는 시간을 가져보려 한다.</p>
<p>Flux 패턴은 2014년 페이스북 F8 컨퍼런스에서 발표된 아키텍처로, Client-Side 웹 애플리케이션을 만들기 위해 사용하는 디자인 패턴이다.</p>
<p>단방향 데이터 흐름(Unidirectional Data Flow)을 특징으로 하며 기존 MVC 패턴의 복잡한 데이터 흐름 문제를 해결하기 위해 고안되었다.</p>
<h3 id="mvc는-무엇인가">MVC는 무엇인가?</h3>
<p>MVC 패턴은 백엔드 아키텍쳐에서 주로 사용되는 디자인 패턴으로 모델 뷰 컨트롤러로 분리되어 있다.
백엔드에서의 작업 수행 절차는</p>
<ul>
<li>client의 request를 받는다.</li>
<li>request를 분석한다.</li>
<li>필요한 데이터를 수집/가공한다.</li>
<li>view를 생성해 response를 client에 전달한다.</li>
</ul>
<p>식으로 이루어져 있는데,</p>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/d6867bb5-bb7f-438c-b5b4-b0d568a9c37b/image.png" />
순서대로 나열하면 이러한 하나의 흐름을 갖는다.</p>
<p><strong>여기서 문제점이 발생하는데 이러한 구조는 강한 의존성이 요구된다는 것이다.
각각의 레이어들이 다음 단계에 있는 레이어의 존재를 알고 있어야 한다.</strong></p>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/8347d1fb-7a34-4549-ba73-27a88291c285/image.png" /></p>
<p>따라서 컨트롤러를 통해 Model과 View 간의 의존성을 어느정도 없애고 상호작용을 할 수 있다.</p>
<p>하지만 애플리케이션의 규모가 커진다면 문제가 발생한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/70b5df01-6e3b-4b27-bfda-214173b4f7d9/image.png" /></p>
<p><strong>프론트엔드에서의 View는 mvc패턴에서의 View와 조금 다른 성격을 가지고 있다.</strong></p>
<ul>
<li>MVC패턴에서의 View는 Model에서 만들어낸 response를 보여주는 역할을 한다.</li>
<li>하지만 프론트엔드에서의 View는 이벤트의 발생지로 메인이자 controller의 역할을 맡는다.</li>
<li>그러므로 애플리케이션 내에 View가 매우 많이 존재한다.</li>
<li>따라서 Model과 View가 양방향의 구조를 가지게 된다면 복잡도가 상당히 올라가고, 이벤트가 애플리케이션 전체로 퍼져나갈 때 이를 예측하기 힘들어진다.</li>
</ul>
<p>이에 대한 해결방안으로 Facebook에서 단방향 구조를 가진 Flux 패턴을 고안해냈다.</p>
<h3 id="flux-패턴의-구조">Flux 패턴의 구조</h3>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/431d1488-45cf-4c48-99af-65e4bb78dad2/image.png" /></p>
<ul>
<li>Action: 데이터 변경에 대한 명세</li>
<li>Dispatcher: Action을 Store로 전달하는 중앙 허브</li>
<li>Store: 애플리케이션의 상태와 로직을 관리</li>
<li>View: Store의 상태를 화면에 표시</li>
</ul>
<h3 id="mvc-패턴과-flux-패턴의-차이점을-투두-리스트-예시를-통해-알아보자">MVC 패턴과 Flux 패턴의 차이점을 투두 리스트 예시를 통해 알아보자</h3>
<ul>
<li><p>투두 앱에서 할 일 목록을 보여주려면 백엔드 서버에서 데이터를 가져와야 한다.</p>
</li>
<li><p>서버에서 가져오는 코드(함수)나 할 일 목록은 모델에 해당한다. </p>
</li>
<li><p>할 일을 추가하려면 서버에 데이터를 보내는 코드가 필요하다. 
(React 기준에서는 모델 대신 보통 Redux, Zustand 같은 스토어(중앙 집중식 상태 관리)를 사용)</p>
<pre><code class="language-js">// /models/todo.js
class TodoModel {
constructor() {
  this.todos = this.getTodos()
}
async fetchTodos() {
  const res = await fetch('&lt;https://todos.com&gt;', {
    method: 'GET',
  })
  return res.json()
}
async createTodo(title) {
  const res = await fetch('&lt;https://todos.com&gt;', {
    method: 'POST',
    body: JSON.stringify({ title })
  })
  return res.json()
}
}</code></pre>
<p>화면에 할 일 목록을 출력하는 코드와 할 일을 추가하기 위해 사용자에게 데이터를 입력받는 화면의 내용(인풋 요소 등)도 필요하다. 
MVC 패턴에서는 오로지 화면에 출력되거나 화면에서 발생하는 이벤트만 등록한다. 
(React.js 같은 모던 프론트엔드 프레임워크 기준에서는 뷰 대신 보통 컴포넌트를 사용)</p>
<pre><code class="language-js">// /views/todo.js
class TodoView {
constructor(root) {
  this.appEl = document.querySelector(root)
  this.formEl = document.createElement('form')
  this.inputEl = document.createElement('input')
  this.todosEl = document.createElement('ul')

  this.formEl.append(this.inputEl)
  this.appEl.append(this.formEl, this.todosEl)
}
renderTodos(todos) {
  const todosEl = todos.map(todo =&gt; {
    const todoEl = document.createElement('li')
    todoEl.textContent = todo.title
    return todoEl
  })
  this.todosEl.innerHTML = ''
  this.todosEl.append(...todoEls)
}
bindAddTodo(handler) {
  this.formEl.addEventListener('submit', handler)
}
}</code></pre>
<p>이렇게 서로 독립된 각 모델과 뷰를 연결할 수 있는 컨트롤러가 필요하게 된다.</p>
<pre><code class="language-js">// /controllers/todo.js
class TodoController {
constructor(model, view) {
  // 각 독립된 모델과 뷰를 컨트롤러에서 초기화
  this.model = model
  this.view = view

  this.view.bindAddTodo(this.handleAddTodo) // 모델을 사용하는 handleAddTodo 이벤트 핸들러를 뷰에 전달해서 등록!
  this.view.renderTodos(this.model.todos) // 모델의 데이터를 뷰에 전달해서 출력!
}
async handleAddTodo(event) {
  event.preventDefault()
  const title = this.view.inputEl.value
  await this.model.createTodo(title)
  await this.model.fetchTodos()
  this.view.renderTodos(this.model.todos)
}
}</code></pre>
<p>이제 이렇게 구성된 모델, 뷰, 컨트롤러로 투두 앱을 구현할 수 있습니다. 
(React.js 같은 모던 프론트엔드 프레임워크 기준에서는 보통 뷰와 컨트롤러가 하나의 컴포넌트에 포함된다.)</p>
<pre><code class="language-js">// /main.js
import TodoModel from './models/todo.js'
import TodoView from './views/todo.js'
import TodoController from './controllers/todo.js'
</code></pre>
</li>
</ul>
<p>const model = new TodoModel()
const view = new TodoView()
const controller = new TodoController(model, view)</p>
<pre><code>이렇듯 모델과 뷰는 서로 독립적으로 서로의 코드가 섞이면 안 된다. 
컨트롤러는 모델과 뷰를 연결해서 말 그대로 컨트롤하는 역할을 한다. 

**Flux 패턴에서는 다음과 같은 방법으로 구현할 수 있다.**
```js
// 가능한 모든 액션들을 상수로 정의
export const INCREMENT = 'INCREMENT';
export const DECREMENT = 'DECREMENT';
export const RESET = 'RESET';
export const SET_VALUE = 'SET_VALUE';</code></pre><pre><code class="language-js">// 액션 객체를 생성하는 함수들
export const counterActions = {
  increment: () =&gt; ({
    type: INCREMENT
  }),
  decrement: () =&gt; ({
    type: DECREMENT
  })
  // ...
};</code></pre>
<pre><code class="language-js">// Zustand를 사용한 상태 관리
export const useCounterStore = create((set) =&gt; ({
  count: 0,
  history: [],
  dispatch: (action) =&gt; {
    // 상태 변경 로직
  }
}));</code></pre>
<pre><code class="language-js">const Counter = () =&gt; {
  const { count, dispatch } = useCounterStore();

  const handleIncrement = () =&gt; {
    dispatch(counterActions.increment());
  };
  // ...
};</code></pre>
<p>사용자가 '+' 버튼을 클릭하면 handleIncrement 함수가 호출되고 INCREMENT 액션이 생성되어 dispatch된다. 
이때 Store가 액션을 받아 상태를 업데이트하고 업데이트된 상태가 다시 컴포넌트로 전달되어 화면을 갱신한다.</p>
<hr />
<p>이러한 구조로 인해 Flux 패턴은 단방향 데이터 흐름을 가진 React와 궁합이 좋고, 컴포넌트 간 데이터 전달 용이하며 상태 변화 추적이 용이하다는 장점이 있다.</p>
<p>React의 여러 상태관리 역시 Flux 패턴을 구현하여 만들어졌다.</p>
<p>대표적으로 Redux와 zustand가 있다.</p>
<h4 id="참고자료">참고자료</h4>
<ul>
<li><a href="https://medium.com/hcleedev/web-react-flux-%ED%8C%A8%ED%84%B4-88d6caa13b5b">https://medium.com/hcleedev/web-react-flux-%ED%8C%A8%ED%84%B4-88d6caa13b5b</a></li>
<li><a href="https://velog.io/@andy0011/Flux-%ED%8C%A8%ED%84%B4%EC%9D%B4%EB%9E%80">https://velog.io/@andy0011/Flux-%ED%8C%A8%ED%84%B4%EC%9D%B4%EB%9E%80</a></li>
<li><a href="https://haruair.github.io/flux/docs/overview.html">https://haruair.github.io/flux/docs/overview.html</a></li>
<li><a href="https://www.youtube.com/watch?v=Y5vOfv67h8A">https://www.youtube.com/watch?v=Y5vOfv67h8A</a></li>
</ul>