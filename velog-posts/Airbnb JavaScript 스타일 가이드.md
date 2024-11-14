<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/514135ca-d5c1-49bb-804b-55daa77248d7/image.png" /></p>
<h2 id="형types">형(Types)</h2>
<p>1.1 Primitives: primitive type은 그 값을 직접 조작합니다.</p>
<ul>
<li>string</li>
<li>number</li>
<li>boolean</li>
<li>null</li>
<li>undefined</li>
</ul>
<pre><code class="language-js">const foo = 1;
let bar = foo;

bar = 9;

console.log(foo, bar); // =&gt; 1, 9</code></pre>
<p>1.2 참조형: 참조형(Complex)은 참조를 통해 값을 조작합니다.</p>
<ul>
<li>object</li>
<li>array</li>
<li>function</li>
</ul>
<pre><code class="language-js">const foo = [1, 2];
const bar = foo;

bar[0] = 9;

console.log(foo[0], bar[0]); // =&gt; 9, 9</code></pre>
<h2 id="참조reference">참조(Reference)</h2>
<p>2.1 모든 참조는 const 를 사용하고, var 를 사용하지 마십시오.</p>
<pre><code class="language-js">// bad
var a = 1;
var b = 2;

// good
const a = 1;
const b = 2;</code></pre>
<p>2.2 참조를 재할당 해야한다면 var 대신 let 을 사용하십시오.</p>
<pre><code class="language-js">// bad
var count = 1;
if (true) {
  count += 1;
}

// good, use the let.
let count = 1;
if (true) {
  count += 1;
}</code></pre>
<p>2.3 let 과 const 는 블록스코프라는것을 유의하십시오.</p>
<pre><code class="language-js">// const and let only exist in the blocks they are defined in.
// const 와 let 은 선언된 블록의 안에서만 존재합니다.
{
  let a = 1;
  const b = 1;
}
console.log(a); // ReferenceError
console.log(b); // ReferenceError</code></pre>
<h2 id="오브젝트objects">오브젝트(Objects)</h2>
<p>3.1 오브젝트를 작성할때는, 리터럴 구문을 사용하십시오.</p>
<pre><code class="language-js">// bad
const item = new Object();

// good
const item = {};</code></pre>
<p>3.2 코드가 브라우저상의 스크립트로 실행될때 예약어를 키로 이용하지 마십시오. IE8에서 작동하지 않습니다. More info 하지만 ES6 모듈안이나 서버사이드에서는 이용가능합니다.</p>
<pre><code class="language-js">// bad
const superman = {
  default: { clark: 'kent' },
  private: true,
};

// good
const superman = {
  defaults: { clark: 'kent' },
  hidden: true,
};</code></pre>
<p>3.3 예약어 대신 알기쉬운 동의어를 사용해 주십시오.</p>
<pre><code class="language-js">// bad
const superman = {
  class: 'alien',
};

// bad
const superman = {
  klass: 'alien',
};

// good
const superman = {
  type: 'alien',
};</code></pre>
<p>3.4 동적 프로퍼티명을 갖는 오브젝트를 작성할때, 계산된 프로퍼티명을 이용해 주십시오.</p>
<pre><code class="language-js">function getKey(k) {
  return a `key named ${k}`;
}

// bad
const obj = {
  id: 5,
  name: 'San Francisco',
};
obj[getKey('enabled')] = true;

// good
const obj = {
  id: 5,
  name: 'San Francisco',
  ［getKey('enabled')]: true
};</code></pre>
<p>3.5 메소드의 단축구문을 이용해 주십시오.</p>
<pre><code class="language-js">// bad
const atom = {
  value: 1,

  addValue: function (value) {
    return atom.value + value;
  },
};

// good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  },
};</code></pre>
<p>3.6 프로퍼티의 단축구문을 이용해 주십시오.</p>
<pre><code class="language-js">const lukeSkywalker = 'Luke Skywalker';

// bad
const obj = {
  lukeSkywalker: lukeSkywalker,
};

// good
const obj = {
  lukeSkywalker,
};</code></pre>
<p>3.7 프로퍼티의 단축구문은 오브젝트 선언의 시작부분에 그룹화 해주십시오.</p>
<pre><code class="language-js">const anakinSkywalker = 'Anakin Skywalker';
const lukeSkywalker = 'Luke Skywalker';

// bad
const obj = {
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  lukeSkywalker,
  episodeThree: 3,
  mayTheFourth: 4,
  anakinSkywalker,
};

// good
const obj = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4,
};</code></pre>
<h2 id="배열arrays">배열(Arrays)</h2>
<p>4.1 배열을 작성 할 때는 리터럴 구문을 사용해 주십시오.</p>
<pre><code class="language-js">// bad
const items = new Array();

// good
const items = [];</code></pre>
<p>4.2 직접 배열에 항목을 대입하지 말고, Array#push를 이용해 주십시오.</p>
<pre><code class="language-js">const someStack = [];

// bad
someStack[someStack.length] = 'abracadabra';

// good
someStack.push('abracadabra');</code></pre>
<p>4.3 배열을 복사할때는 배열의 확장연산자 ... 를 이용해 주십시오.</p>
<pre><code class="language-js">// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i &lt; len; i++) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];</code></pre>
<p>4.4 array-like 오브젝트를 배열로 변환하는 경우는 Array#from을 이용해 주십시오.</p>
<pre><code class="language-js">const foo = document.querySelectorAll('.foo');
const nodes = Array.from(foo);</code></pre>
<h2 id="구조화대입destructuring">구조화대입(Destructuring)</h2>
<p>5.1 하나의 오브젝트에서 복수의 프로퍼티를 억세스 할 때는 오브젝트 구조화대입을 이용해 주십시오.</p>
<pre><code class="language-js">// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
}

// good
function getFullName(obj) {
  const { firstName, lastName } = obj;
  return `${firstName} ${lastName}`;
}

// best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}</code></pre>
<p>5.2 배열의 구조화대입을 이용해 주십시오.</p>
<pre><code class="language-js">const arr = [1, 2, 3, 4];

// bad
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;</code></pre>
<h2 id="문자열strings">문자열(Strings)</h2>
<p>6.1 문자열에는 싱크쿼트 '' 를 사용해 주십시오.</p>
<pre><code class="language-js">// bad
const name = "Capt. Janeway";

// good
const name = 'Capt. Janeway';</code></pre>
<p>6.2 100문자 이상의 문자열은 문자열연결을 사용해서 복수행에 걸쳐 기술할 필요가 있습니다.
6.3 주의: 문자연결을 과용하면 성능에 영향을 미칠 수 있습니다. jsPerf &amp; Discussion.</p>
<pre><code class="language-js">// bad
const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

// bad
const errorMessage = 'This is a super long error that was thrown because \
of Batman. When you stop to think about how Batman had anything to do \
with this, you would get nowhere \
fast.';

// good
const errorMessage = 'This is a super long error that was thrown because ' +
  'of Batman. When you stop to think about how Batman had anything to do ' +
  'with this, you would get nowhere fast.';</code></pre>
<p>6.4 프로그램에서 문자열을 생성하는 경우는 문자열 연결이 아닌 template strings를 이용해 주십시오.</p>
<pre><code class="language-js">// bad
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

// bad
function sayHi(name) {
  return ['How are you, ', name, '?'].join();
}

// good
function sayHi(name) {
  return `How are you, ${name}?`;
}</code></pre>
<p>6.5 절대로 eval() 을 이용하지 마십시오. 이것은 많은 취약점을 만들기 때문입니다.</p>
<h2 id="함수functions">함수(Functions)</h2>
<p>7.1 함수식 보다 함수선언을 이용해 주십시오.</p>
<pre><code class="language-js">// bad
const foo = function () {
};

// good
function foo() {
}</code></pre>
<p>7.2 함수식</p>
<pre><code class="language-js">// immediately-invoked function expression (IIFE)
// 즉시 실행 함수식(IIFE)
(() =&gt; {
  console.log('Welcome to the Internet. Please follow me.');
})();</code></pre>
<p>7.3 함수이외의 블록 (if나 while같은) 안에서 함수를 선언하지 마십시오. 변수에 함수를 대입하는 대신 브라우저들은 그것을 허용하지만 모두가 다르게 해석합니다.</p>
<p>7.4 주의: ECMA-262 사양에서는 block 은 statements의 일람으로 정의되어 있지만 함수선언은 statements 가 아닙니다. Read ECMA-262's note on this issue.</p>
<pre><code class="language-js">// bad
if (currentUser) {
  function test() {
    console.log('Nope.');
  }
}

// good
let test;
if (currentUser) {
  test = () =&gt; {
    console.log('Yup.');
  };
}</code></pre>
<p>7.5 절대 파라미터에 arguments 를 지정하지 마십시오. 이것은 함수스코프에 전해지는 arguments 오브젝트의 참조를 덮어써 버립니다.</p>
<pre><code class="language-js">// bad
function nope(name, options, arguments) {
  // ...stuff...
}

// good
function yup(name, options, args) {
  // ...stuff...
}</code></pre>
<p>7.6 절대 arguments 를 이용하지 마십시오. 대신에 rest syntax ... 를 이용해 주십시오.</p>
<pre><code class="language-js">// bad
function concatenateAll() {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
}

// good
function concatenateAll(...args) {
  return args.join('');
}</code></pre>
<p>7.7 함수의 파라미터를 변이시키는 것보다 default 파라미터를 이용해 주십시오.</p>
<pre><code class="language-js">// really bad
function handleThings(opts) {
  // 안돼！함수의 파라메터를 변이시키면 안됩니다.
  // 만약 opts가 falsy 하다면 바라는데로 오브젝트가 설정됩니다.
  // 하지만 미묘한 버그를 일으킬지도 모릅니다.
  opts = opts || {};
  // ...
}

// still bad
function handleThings(opts) {
  if (opts === void 0) {
    opts = {};
  }
  // ...
}

// good
function handleThings(opts = {}) {
  // ...
}</code></pre>
<p>7.8 side effect가 있을 default 파라메터의 이용은 피해 주십시오.</p>
<pre><code class="language-js">var b = 1;
// bad
function count(a = b++) {
  console.log(a);
}
count();  // 1
count();  // 2
count(3); // 3
count();  // 3</code></pre>
<p>7.9 항상 default 파라메터는 뒤쪽에 두십시오.</p>
<pre><code class="language-js">// bad
function handleThings(opts = {}, name) {
  // ...
}

// good
function handleThings(name, opts = {}) {
  // ...
}</code></pre>
<p>7.10 절대 새 함수를 작성하기 위해 Function constructor를 이용하지 마십시오.</p>
<pre><code class="language-js">// bad
var add = new Function('a', 'b', 'return a + b');

// still bad
var subtract = Function('a', 'b', 'return a - b');</code></pre>
<h2 id="arrow함수arrow-functions">Arrow함수(Arrow Functions)</h2>
<p>8.1 (무명함수를 전달하는 듯한)함수식을 이용하는 경우 arrow함수 표기를 이용해 주십시오.</p>
<pre><code class="language-js">// bad
[1, 2, 3].map(function (x) {
  const y = x + 1;
  return x * y;
});

// good
[1, 2, 3].map((x) =&gt; {
  const y = x + 1;
  return x * y;
});</code></pre>
<p>8.2 함수의 본체가 하나의 식으로 구성된 경우에는 중괄호({})를 생략하고 암시적 return을 이용하는것이 가능합니다. 그 외에는 return 문을 이용해 주십시오.</p>
<pre><code class="language-js">// good
[1, 2, 3].map(number =&gt; `A string containing the ${number}.`);

// bad
[1, 2, 3].map(number =&gt; {
  const nextNumber = number + 1;
  `A string containing the ${nextNumber}.`;
});

// good
[1, 2, 3].map(number =&gt; {
  const nextNumber = number + 1;
  return `A string containing the ${nextNumber}.`;
});</code></pre>
<p>8.3 식이 복수행에 걸쳐있을 경우는 가독성을 더욱 좋게하기 위해 소괄호()로 감싸 주십시오.</p>
<pre><code class="language-js">// bad
[1, 2, 3].map(number =&gt; 'As time went by, the string containing the ' +
  `${number} became much longer. So we needed to break it over multiple ` +
  'lines.'
);

// good
[1, 2, 3].map(number =&gt; (
  `As time went by, the string containing the ${number} became much ` +
  'longer. So we needed to break it over multiple lines.'
));</code></pre>
<p>8.4 함수의 인수가 하나인 경우 소괄호()를 생략하는게 가능합니다.</p>
<pre><code class="language-js">// good
[1, 2, 3].map(x =&gt; x * x);

// good
[1, 2, 3].reduce((y, x) =&gt; x + y);</code></pre>
<h2 id="classes--constructors">Classes &amp; Constructors</h2>
<p>9.1 prototype 을 직접 조작하는것을 피하고 항상 class 를 이용해 주십시오.</p>
<pre><code class="language-js">// bad
function Queue(contents = []) {
  this._queue = [...contents];
}
Queue.prototype.pop = function() {
  const value = this._queue[0];
  this._queue.splice(0, 1);
  return value;
}

// good
class Queue {
  constructor(contents = []) {
    this._queue = [...contents];
  }
  pop() {
    const value = this._queue[0];
    this._queue.splice(0, 1);
    return value;
  }
}</code></pre>
<p>9.2 상속은 extends 를 이용해 주십시오.</p>
<pre><code class="language-js">// bad
const inherits = require('inherits');
function PeekableQueue(contents) {
  Queue.apply(this, contents);
}
inherits(PeekableQueue, Queue);
PeekableQueue.prototype.peek = function() {
  return this._queue[0];
}

// good
class PeekableQueue extends Queue {
  peek() {
    return this._queue[0];
  }
}</code></pre>
<p>9.3 메소드의 반환값으로 this 를 반환하는 것으로 메소드채이닝을 할 수 있습니다.</p>
<pre><code class="language-js">// bad
Jedi.prototype.jump = function() {
  this.jumping = true;
  return true;
};

Jedi.prototype.setHeight = function(height) {
  this.height = height;
};

const luke = new Jedi();
luke.jump(); // =&gt; true
luke.setHeight(20); // =&gt; undefined

// good
class Jedi {
  jump() {
    this.jumping = true;
    return this;
  }

  setHeight(height) {
    this.height = height;
    return this;
  }
}

const luke = new Jedi();

luke.jump()
  .setHeight(20);</code></pre>
<p>9.4 독자의 toString()을 작성하는것을 허용하지만 올바르게 동작하는지와 side effect 가 없는지만 확인해 주십시오.</p>
<pre><code class="language-js">class Jedi {
  constructor(options = {}) {
    this.name = options.name || 'no name';
  }

  getName() {
    return this.name;
  }

  toString() {
    return `Jedi - ${this.getName()}`;
  }
}</code></pre>
<h2 id="모듈modules">모듈(Modules)</h2>
<p>10.1 비표준 모듈시스템이 아닌 항상 (import/export) 를 이용해 주십시오. 이렇게 함으로써 선호하는 모듈시스템에 언제라도 옮겨가는게 가능해 집니다.</p>
<pre><code class="language-js">// bad
const AirbnbStyleGuide = require('./AirbnbStyleGuide');
module.exports = AirbnbStyleGuide.es6;

// ok
import AirbnbStyleGuide from './AirbnbStyleGuide';
export default AirbnbStyleGuide.es6;

// best
import { es6 } from './AirbnbStyleGuide';
export default es6;</code></pre>
<p>10.2 wildcard import 는 이용하지 마십시오.</p>
<pre><code class="language-js">// bad
import * as AirbnbStyleGuide from './AirbnbStyleGuide';

// good
import AirbnbStyleGuide from './AirbnbStyleGuide';</code></pre>
<p>10.3 import 문으로부터 직접 export 하는것은 하지말아 주십시오.</p>
<pre><code class="language-js">// bad
// filename es6.js
export { es6 as default } from './airbnbStyleGuide';

// good
// filename es6.js
import { es6 } from './AirbnbStyleGuide';
export default es6;</code></pre>
<h2 id="이터레이터와-제너레이터iterators-and-generators">이터레이터와 제너레이터(Iterators and Generators)</h2>
<p>11.1 iterators를 이용하지 마십시오. for-of 루프 대신에 map() 과 reduce() 와 같은 JavaScript 고급함수(higher-order functions)를 이용해 주십시오.</p>
<pre><code class="language-js">const numbers = [1, 2, 3, 4, 5];

// bad
let sum = 0;
for (let num of numbers) {
  sum += num;
}

sum === 15;

// good
let sum = 0;
numbers.forEach((num) =&gt; sum += num);
sum === 15;

// best (use the functional force)
const sum = numbers.reduce((total, num) =&gt; total + num, 0);
sum === 15;</code></pre>
<p>11.2 현시점에서는 generators는 이용하지 마십시오.</p>
<h2 id="프로퍼티properties">프로퍼티(Properties)</h2>
<p>12.1 프로퍼티에 억세스하는 경우는 점 . 을 사용해 주십시오.</p>
<pre><code class="language-js">const luke = {
  jedi: true,
  age: 28,
};

// bad
const isJedi = luke['jedi'];

// good
const isJedi = luke.jedi;</code></pre>
<p>12.2 변수를 사용해 프로퍼티에 억세스하는 경우는 대괄호 [] 를 사용해 주십시오.</p>
<pre><code class="language-js">const luke = {
  jedi: true,
  age: 28,
};

function getProp(prop) {
  return luke[prop];
}

const isJedi = getProp('jedi');</code></pre>
<h2 id="변수variables">변수(Variables)</h2>
<p>13.1 변수를 선언 할 때는 항상 const 를 사용해 주십시오. 그렇게 하지 않으면 글로벌 변수로 선언됩니다. 글로벌 namespace 를 오염시키지 않도록 캡틴플래닛도 경고하고 있습니다.</p>
<pre><code class="language-js">// bad
superPower = new SuperPower();

// good
const superPower = new SuperPower();</code></pre>
<p>13.2 하나의 변수선언에 대해 하나의 const 를 이용해 주십시오.</p>
<pre><code class="language-js">// bad
const items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';

// bad
// (compare to above, and try to spot the mistake)
const items = getItems(),
    goSportsTeam = true;
    dragonball = 'z';

// good
const items = getItems();
const goSportsTeam = true;
const dragonball = 'z';</code></pre>
<p>13.3 우선 const 를 그룹화하고 다음에 let 을 그룹화 해주십시오.</p>
<pre><code class="language-js">// bad
let i, len, dragonball,
    items = getItems(),
    goSportsTeam = true;

// bad
let i;
const items = getItems();
let dragonball;
const goSportsTeam = true;
let len;

// good
const goSportsTeam = true;
const items = getItems();
let dragonball;
let i;
let length;</code></pre>
<p>13.4 변수를 할당할때는 필요하고 합리적인 장소에 두시기 바랍니다.</p>
<pre><code class="language-js">// good
function() {
  test();
  console.log('doing stuff..');

  //..other stuff..

  const name = getName();

  if (name === 'test') {
    return false;
  }

  return name;
}

// bad - unnecessary function call
// 필요없는 함수 호출
function(hasName) {
  const name = getName();

  if (!hasName) {
    return false;
  }

  this.setFirstName(name);

  return true;
}

// good
function(hasName) {
  if (!hasName) {
    return false;
  }

  const name = getName();
  this.setFirstName(name);

  return true;
}</code></pre>
<h2 id="호이스팅">호이스팅</h2>
<p>14.1 var 선언은 할당이 없이 스코프의 선두에 hoist 됩니다. const 와 let 선언은Temporal Dead Zones (TDZ) 라고 불리는 새로운 컨셉의 혜택을 받고 있습니다. 이것은 왜 typeof 는 더이상 안전하지 않은가를 알고있는 것이 중요합니다.</p>
<pre><code class="language-js">// we know this wouldn't work (assuming there
// is no notDefined global variable)
// (notDefined 가 글로벌변수에 존재하지 않는다고 판정한 경우.)
// 잘 동작하지 않습니다.
function example() {
  console.log(notDefined); // =&gt; throws a ReferenceError
}

// creating a variable declaration after you
// reference the variable will work due to
// variable hoisting. Note: the assignment
// value of `true` is not hoisted.
// 그 변수를 참조하는 코드의 뒤에서 그 변수를 선언한 경우
// 변수가 hoist 된 상태에서 동작합니다..
// 주의：`true` 라는 값 자체는 hoist 되지 않습니다.
function example() {
  console.log(declaredButNotAssigned); // =&gt; undefined
  var declaredButNotAssigned = true;
}

// The interpreter is hoisting the variable
// declaration to the top of the scope,
// which means our example could be rewritten as:
// 인터프리터는 변수선언을 스코프의 선두에 hoist 합니다.
// 위의 예는 다음과 같이 다시 쓸수 있습니다.
function example() {
  let declaredButNotAssigned;
  console.log(declaredButNotAssigned); // =&gt; undefined
  declaredButNotAssigned = true;
}

// using const and let
// const 와 let 을 이용한 경우
function example() {
  console.log(declaredButNotAssigned); // =&gt; throws a ReferenceError
  console.log(typeof declaredButNotAssigned); // =&gt; throws a ReferenceError
  const declaredButNotAssigned = true;
}</code></pre>
<p>14.2 무명함수의 경우 함수가 할당되기 전의 변수가 hoist 됩니다.</p>
<pre><code class="language-js">function example() {
  console.log(anonymous); // =&gt; undefined

  anonymous(); // =&gt; TypeError anonymous is not a function

  var anonymous = function() {
    console.log('anonymous function expression');
  };
}</code></pre>
<p>14.3 명명함수의 경우도 똑같이 변수가 hoist 됩니다. 함수명이나 함수본체는 hoist 되지 않습니다.</p>
<pre><code class="language-js">function example() {
  console.log(named); // =&gt; undefined

  named(); // =&gt; TypeError named is not a function

  superPower(); // =&gt; ReferenceError superPower is not defined

  var named = function superPower() {
    console.log('Flying');
  };
}

// the same is true when the function name
// is the same as the variable name.
// 함수명과 변수명이 같은 경우도 같은 현상이 발생합니다.
function example() {
  console.log(named); // =&gt; undefined

  named(); // =&gt; TypeError named is not a function

  var named = function named() {
    console.log('named');
  }
}</code></pre>
<p>14.4 함수선언은 함수명과 함수본체가 호이스트 됩니다.</p>
<pre><code class="language-js">function example() {
  superPower(); // =&gt; Flying

  function superPower() {
    console.log('Flying');
  }
}</code></pre>
<h2 id="조건식과-등가식comparison-operators--equality">조건식과 등가식(Comparison Operators &amp; Equality)</h2>
<p>15.1 == 이나 != 보다 === 와 !== 을 사용해 주십시오.
15.2 if 문과 같은 조건식은 ToBoolean 메소드에 의한 강제형변환으로 평가되어 항상 다음과 같은 심플한 룰을 따릅니다.</p>
<ul>
<li>오브젝트 는 true 로 평가됩니다.</li>
<li>undefined 는 false 로 평가됩니다.</li>
<li>null 은 false 로 평가됩니다.</li>
<li>부울값 은 boolean형의 값 으로 평가됩니다.</li>
<li>수치 는 true 로 평가됩니다. 하지만 +0, -0, or NaN 의 경우는 false 입니다.</li>
<li>문자열 은 true 로 평가됩니다. 하지만 빈문자 '' 의 경우는 false 입니다.</li>
</ul>
<p>15.3 단축형을 사용해 주십시오.</p>
<pre><code class="language-js">// bad
if (name !== '') {
  // ...stuff...
}

// good
if (name) {
  // ...stuff...
}

// bad
if (collection.length &gt; 0) {
  // ...stuff...
}

// good
if (collection.length) {
  // ...stuff...
}</code></pre>
<h2 id="블록blocks">블록(Blocks)</h2>
<p>16.1 복수행의 블록에는 중괄호 ({}) 를 사용해 주십시오.</p>
<pre><code class="language-js">// bad
if (test)
  return false;

// good
if (test) return false;

// good
if (test) {
  return false;
}

// bad
function() { return false; }

// good
function() {
  return false;
}</code></pre>
<p>16.2 복수행 블록의 if 와 else 를 이용하는 경우 else 는 if 블록 끝의 중괄호(})와 같은 행에 위치시켜 주십시오.</p>
<pre><code class="language-js">// bad
if (test) {
  thing1();
  thing2();
}
else {
  thing3();
}

// good
if (test) {
  thing1();
  thing2();
} else {
  thing3();
}</code></pre>
<h2 id="코멘트comments">코멘트(Comments)</h2>
<p>17.1 복수행의 코멘트는 /** ... */ 을 사용해 주십시오. 그 안에는 설명과 모든 파라메터, 반환값에 대해 형이나 값을 기술해 주십시오.</p>
<pre><code class="language-js">// bad
// make() returns a new element
// based on the passed in tag name
//
// @param {String} tag
// @return {Element} element
function make(tag) {

  // ...stuff...

  return element;
}

// good
/**
 * make() returns a new element
 * based on the passed in tag name
 *
 * @param {String} tag
 * @return {Element} element
 */
function make(tag) {

  // ...stuff...

  return element;
}</code></pre>
<p>17.2 단일행 코멘트에는 // 을 사용해 주십시오. 코멘트를 추가하고 싶은 코드의 상부에 배치해 주십시오. 또한, 코멘트의 앞에 빈행을 넣어 주십시오.</p>
<pre><code class="language-js">// bad
const active = true;  // is current tab

// good
// is current tab
const active = true;

// bad
function getType() {
  console.log('fetching type...');
  // set the default type to 'no type'
  const type = this._type || 'no type';

  return type;
}

// good
function getType() {
  console.log('fetching type...');

  // set the default type to 'no type'
  const type = this._type || 'no type';

  return type;
}

// also good
function getType() {
  // set the default type to 'no type'
  const type = this._type || 'no type';

  return type;
}</code></pre>
<p>17.3 문제를 지적하고 재고를 촉구하는 경우나 문제의 해결책을 제안하는 경우 등, 코멘트의 앞에 FIXME 나 TODO 를 붙이는 것으로 다른 개발자의 빠른 이해를 도울수 있습니다. 이런것들은 어떤 액션을 따른다는 의미로 통상의 코멘트와는 다릅니다. 액션이라는 것은 FIXME -- 해결이 필요 또는 TODO -- 구현이 필요 를 뜻합니다.</p>
<p>17.4 문제에 대한 주석으로써 // FIXME: 를 사용해 주십시오.</p>
<pre><code class="language-js">class Calculator extends Abacus {
  constructor() {
    super();

    // FIXME: shouldn't use a global here
    // FIXME: 글로벌변수를 사용해서는 안됨.
    total = 0;
  }
}</code></pre>
<p>17.5 문제의 해결책에 대한 주석으로 // TODO: 를 사용해 주십시오.</p>
<pre><code class="language-js">class Calculator extends Abacus {
  constructor() {
    super();

    // TODO: total should be configurable by an options param
    // TODO: total 은 옵션 파라메터로 설정해야함.
    this.total = 0;
  }
}</code></pre>
<h2 id="공백whitespace">공백(Whitespace)</h2>
<p>18.1 탭에는 스페이스 2개를 설정해 주십시오.</p>
<pre><code class="language-js">// bad
function() {
∙∙∙∙const name;
}

// bad
function() {
∙const name;
}

// good
function() {
∙∙const name;
}</code></pre>
<p>18.2 주요 중괄호 ({}) 앞에는 스페이스를 1개 넣어 주십시오.</p>
<pre><code class="language-js">// bad
function test(){
  console.log('test');
}

// good
function test() {
  console.log('test');
}

// bad
dog.set('attr',{
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});

// good
dog.set('attr', {
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});</code></pre>
<p>18.3 제어구문 (if 문이나 while 문 등) 의 소괄호 (()) 앞에는 스페이스를 1개 넣어 주십시오. 함수선언이나 함수호출시 인수리스트의 앞에는 스페이스를 넣지 마십시오.</p>
<pre><code class="language-js">// bad
if(isJedi) {
  fight ();
}

// good
if (isJedi) {
  fight();
}

// bad
function fight () {
  console.log ('Swooosh!');
}

// good
function fight() {
  console.log('Swooosh!');
}</code></pre>
<p>18.4 연산자 사이에는 스페이스를 넣어 주십시오.</p>
<pre><code class="language-js">// bad
const x=y+5;

// good
const x = y + 5;</code></pre>
<p>18.5 파일 끝에는 개행문자를 1개 넣어 주십시오.</p>
<pre><code class="language-js">// bad
(function(global) {
  // ...stuff...
})(this);

// good
(function(global) {
  // ...stuff...
})(this);↵</code></pre>
<p>18.6 길게 메소드를 채이닝하는 경우는 인덴트를 이용해 주십시오. 행이 새로운 문이 아닌 메소드 호출인 것을 강조하기 위해서 선두에 점 (.) 을 배치해 주십시오.</p>
<pre><code class="language-js">// bad
$('#items').find('.selected').highlight().end().find('.open').updateCount();

// bad
$('#items').
  find('.selected').
    highlight().
    end().
  find('.open').
    updateCount();

// good
$('#items')
  .find('.selected')
    .highlight()
    .end()
  .find('.open')
    .updateCount();

// bad
const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').class('led', true)
    .attr('width', (radius + margin) * 2).append('svg:g')
    .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
    .call(tron.led);

// good
const leds = stage.selectAll('.led')
    .data(data)
  .enter().append('svg:svg')
    .classed('led', true)
    .attr('width', (radius + margin) * 2)
  .append('svg:g')
    .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
    .call(tron.led);</code></pre>
<p>18.7 문의 앞과 블록의 뒤에는 빈행을 남겨 주십시오.</p>
<pre><code class="language-js">// bad
if (foo) {
  return bar;
}
return baz;

// good
if (foo) {
  return bar;
}

return baz;

// bad
const obj = {
  foo() {
  },
  bar() {
  },
};
return obj;

// good
const obj = {
  foo() {
  },

  bar() {
  },
};

return obj;

// bad
const arr = [
  function foo() {
  },
  function bar() {
  },
];
return arr;

// good
const arr = [
  function foo() {
  },

  function bar() {
  },
];

return arr;</code></pre>
<p>18.8 블록에 빈행을 끼워 넣지 마십시오.</p>
<pre><code class="language-js">// bad
function bar() {

  console.log(foo);

}

// also bad
if (baz) {

  console.log(qux);
} else {
  console.log(foo);

}

// good
function bar() {
  console.log(foo);
}

// good
if (baz) {
  console.log(qux);
} else {
  console.log(foo);
}</code></pre>
<p>18.9 소괄호()의 안쪽에 스페이스를 추가하지 마십시오.</p>
<pre><code class="language-js">// bad
function bar( foo ) {
  return foo;
}

// good
function bar(foo) {
  return foo;
}

// bad
if ( foo ) {
  console.log(foo);
}

// good
if (foo) {
  console.log(foo);
}</code></pre>
<p>18.10 대괄호([])의 안쪽에 스페이스를 추가하지 마십시오.</p>
<pre><code class="language-js">// bad
const foo = [ 1, 2, 3 ];
console.log(foo[ 0 ]);

// good
const foo = [1, 2, 3];
console.log(foo[0]);</code></pre>
<p>18.11 중괄호({})의 안쪽에 스페이스를 추가해 주십시오.</p>
<pre><code class="language-js">// bad
const foo = {clark: 'kent'};

// good
const foo = { clark: 'kent' };</code></pre>
<h2 id="콤마commas">콤마(Commas)</h2>
<p>19.1 선두의 콤마 X</p>
<pre><code class="language-js">// bad
const story = [
    once
  , upon
  , aTime
];

// good
const story = [
  once,
  upon,
  aTime,
];

// bad
const hero = {
    firstName: 'Ada'
  , lastName: 'Lovelace'
  , birthYear: 1815
  , superPower: 'computers'
};

// good
const hero = {
  firstName: 'Ada',
  lastName: 'Lovelace',
  birthYear: 1815,
  superPower: 'computers',
};</code></pre>
<p>19.2 끝의 콤마 O</p>
<pre><code class="language-js">// bad - git diff without trailing comma
const hero = {
     firstName: 'Florence',
-    lastName: 'Nightingale'
+    lastName: 'Nightingale',
+    inventorOf: ['coxcomb graph', 'modern nursing']
};

// good - git diff with trailing comma
const hero = {
     firstName: 'Florence',
     lastName: 'Nightingale',
+    inventorOf: ['coxcomb chart', 'modern nursing'],
};

// bad
const hero = {
  firstName: 'Dana',
  lastName: 'Scully'
};

const heroes = [
  'Batman',
  'Superman'
];

// good
const hero = {
  firstName: 'Dana',
  lastName: 'Scully',
};

const heroes = [
  'Batman',
  'Superman',
];</code></pre>
<p>세미콜론(Semicolons)</p>
<ul>
<li>Yup<pre><code class="language-js">// bad
(function() {
const name = 'Skywalker'
return name
})()
</code></pre>
</li>
</ul>
<p>// good
(() =&gt; {
  const name = 'Skywalker';
  return name;
})();</p>
<p>// good (guards against the function becoming an argument when two files with IIFEs are concatenated)
// good (즉시함수가 연결된 2개의 파일일때 인수가 되는 부분을 보호합니다.
;(() =&gt; {
  const name = 'Skywalker';
  return name;
})();</p>
<pre><code>
## 형변환과 강제(Type Casting &amp; Coercion)
21.1 문의 선두에서 형의 강제를 행합니다.

21.2 문자열의 경우:
```js
//  =&gt; this.reviewScore = 9;

// bad
const totalScore = this.reviewScore + '';

// good
const totalScore = String(this.reviewScore);</code></pre><p>21.3 숫자의 경우: Number 로 형변환하는 경우는 parseInt 를 이용하고, 항상 형변환을 위한 기수를 인수로 넘겨 주십시오.</p>
<pre><code class="language-js">const inputValue = '4';

// bad
const val = new Number(inputValue);

// bad
const val = +inputValue;

// bad
const val = inputValue &gt;&gt; 0;

// bad
const val = parseInt(inputValue);

// good
const val = Number(inputValue);

// good
const val = parseInt(inputValue, 10);</code></pre>
<p>21.4 어떤 이유로 인해 parseInt 가 bottleneck 이 되어, 성능적인 이유로 Bitshift를 사용할 필요가 있는 경우, 왜(why) 와 무엇(what)의 설명을 코멘트로 해서 남겨 주십시오.</p>
<pre><code class="language-js">// good
/**
 * parseInt was the reason my code was slow.
 * Bitshifting the String to coerce it to a
 * Number made it a lot faster.
 * parseInt 가 원인으로 느렸음.
 * Bitshift를 통한 수치로의 문자열 강제 형변환으로
 * 성능을 개선시킴.
 */
const val = inputValue &gt;&gt; 0;</code></pre>
<p>21.5 주의: bitshift를 사용하는 경우의 주의사항. 수치는 64비트 값으로 표현되어 있으나 bitshift 연산한 경우는 항상 32비트 integer 로 넘겨집니다.(소스). 32비트 이상의 int 를 bitshift 하는 경우 예상치 못한 현상을 야기할 수 있습니다.(토론) 부호가 포함된 32비트 정수의 최대치는 2,147,483,647 입니다.</p>
<pre><code class="language-js">2147483647 &gt;&gt; 0 //=&gt; 2147483647
2147483648 &gt;&gt; 0 //=&gt; -2147483648
2147483649 &gt;&gt; 0 //=&gt; -2147483647</code></pre>
<p>21.6 부울값의 경우:</p>
<pre><code class="language-js">const age = 0;

// bad
const hasAge = new Boolean(age);

// good
const hasAge = Boolean(age);

// good
const hasAge = !!age;</code></pre>
<h2 id="명명규칙naming-conventions">명명규칙(Naming Conventions)</h2>
<p>22.1 한 글자의 이름은 피해 주십시오. 이름으로부터 의도가 읽혀질수 있게 해주십시오.</p>
<pre><code class="language-js">// bad
function q() {
  // ...stuff...
}

// good
function query() {
  // ..stuff..
}</code></pre>
<p>22.2 오브젝트, 함수 그리고 인스턴스에는 camelCase를 사용해 주십시오.</p>
<pre><code class="language-js">// bad
const OBJEcttsssss = {};
const this_is_my_object = {};
function c() {}

// good
const thisIsMyObject = {};
function thisIsMyFunction() {}</code></pre>
<p>22.3 클래스나 constructor에는 PascalCase 를 사용해 주십시오.</p>
<pre><code class="language-js">// bad
function user(options) {
  this.name = options.name;
}

const bad = new user({
  name: 'nope',
});

// good
class User {
  constructor(options) {
    this.name = options.name;
  }
}

const good = new User({
  name: 'yup',
});</code></pre>
<p>22.4 private 프로퍼티명은 선두에 언더스코어 _ 를사용해 주십시오.</p>
<pre><code class="language-js">// bad
this.__firstName__ = 'Panda';
this.firstName_ = 'Panda';

// good
this._firstName = 'Panda';</code></pre>
<p>22.5 this 의 참조를 보존하는것은 피해주십시오. arrow함수나 Function#bind 를 이용해 주십시오.</p>
<pre><code class="language-js">// bad
function foo() {
  const self = this;
  return function() {
    console.log(self);
  };
}

// bad
function foo() {
  const that = this;
  return function() {
    console.log(that);
  };
}

// good
function foo() {
  return () =&gt; {
    console.log(this);
  };
}</code></pre>
<p>22.7 Default export가 함수일 경우, camelCase를 이용해 주십시오. 파일명은 함수명과 동일해야 합니다.</p>
<pre><code class="language-js">function makeStyleGuide() {
}

export default makeStyleGuide;</code></pre>
<p>22.8 singleton / function library / 빈오브젝트를 export 하는 경우, PascalCase를 이용해 주십시오.</p>
<pre><code class="language-js">const AirbnbStyleGuide = {
  es6: {
  }
};

export default AirbnbStyleGuide;</code></pre>
<h2 id="접근자-accessors">접근자 (Accessors)</h2>
<p>23.1 프로퍼티를 위한 접근자 함수는 필수는 아닙니다.
23.2 접근자 함수가 필요한 경우, getVal() 이나 setVal('hello') 로 해주십시오.</p>
<pre><code class="language-js">// bad
dragon.age();

// good
dragon.getAge();

// bad
dragon.age(25);

// good
dragon.setAge(25);</code></pre>
<p>23.3 프로퍼티가 boolean 인 경우, isVal() 이나 hasVal() 로 해주십시오.</p>
<pre><code class="language-js">// bad
if (!dragon.age()) {
  return false;
}

// good
if (!dragon.hasAge()) {
  return false;
}</code></pre>
<p>23.4 일관된 경우, get() 과 set() 으로 함수를 작성해도 좋습니다.</p>
<pre><code class="language-js">class Jedi {
  constructor(options = {}) {
    const lightsaber = options.lightsaber || 'blue';
    this.set('lightsaber', lightsaber);
  }

  set(key, val) {
    this[key] = val;
  }

  get(key) {
    return this[key];
  }
}</code></pre>
<h2 id="이벤트events">이벤트(Events)</h2>
<p>24.1 (DOM이벤트나 Backbone events 와 같은 독자의) 이벤트로 payload의 값을 넘길 경우는 raw값 보다는 해시값을 넘겨 주십시오. 이렇게 함으로써, 이후 기여자가 이벤트에 관련한 모든 핸들러를 찾아서 갱신하는 대신 이벤트 payload에 값을 추가하는 것이 가능합니다. </p>
<pre><code class="language-js">// bad
$(this).trigger('listingUpdated', listing.id);

...

$(this).on('listingUpdated', function(e, listingId) {
  // do something with listingId
});

// good
$(this).trigger('listingUpdated', { listingId: listing.id });

...

$(this).on('listingUpdated', function(e, data) {
  // do something with data.listingId
});</code></pre>