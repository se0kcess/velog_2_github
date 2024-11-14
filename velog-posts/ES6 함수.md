<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/4bed5c45-b2e6-4796-ba2b-64e86d239ed4/image.png" /></p>
<h3 id="es6-이전-함수">ES6 이전 함수</h3>
<p>일반 함수로서 호출할 수 있으며 생성자 함수로 호출 가능 (callable &amp; constructor)</p>
<h3 id="callable과-constructornon-constructor">callable과 constructor/non-constructor</h3>
<p>호출할 수 있는 함수 객체를 callable이라 하며 인스턴스를 생성할 수 있는 함수 객체를 constructor,
인스턴스를 생성할 수 없는 객체를 non-constructor라고 부른다.</p>
<pre><code class="language-javascript">var foo = function () {
  return 1;
};

// 일반적인 함수로서 호출
foo(); // -&gt; 1

// 생성자 함수로서 호출
new foo(); // -&gt; foo {}

// 메서드로서 호출
var obj = { foo: foo };
obj.foo(); // -&gt; 1</code></pre>
<blockquote>
<p>ES6 이전의 모든 함수는 사용 목적에 따라 명확한 구분이 없으므로 호출 방식에 특별한 제약이 없고 생성자 함수로 호출되지 않아도 프로토타입 객체를 생성한다.</p>
</blockquote>
<p>ES6에서는 이러한 문제를 해결하기 위해 함수를 사용 목적에 따라 세 가지 종류로 명확히 구분했다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/5b3365e5-4061-44aa-ae8a-89b6ff520ddb/image.png" /></p>
<h3 id="메서드">메서드</h3>
<ul>
<li><p>ES6 이전 사양에는 메서드에 대한 명확한 정의가 없었으나 ES6 사양에서는 <strong>메서드 축약 표현으로 정의된 함수</strong>만을 메서드로 의미한다.</p>
</li>
<li><p><strong>메서드는 인스턴스를 생성할 수 없는 non-constructor이다.</strong></p>
</li>
<li><p>ES6 메서드는 인스턴스를 생성할 수 없으므로 prototype 프로퍼티가 없고 프로토타입도 생성하지 않는다.</p>
</li>
<li><p>ES6 메서드는 자신을 바인딩한 객체를 가리키는 내부 슬롯 [[HomeObject]]를 갖는다.</p>
</li>
</ul>
<p>-ES6 메서드가 아닌 함수는 super 키워드를 사용할 수 없다.</p>
<h3 id="화살표-함수">화살표 함수</h3>
<ul>
<li>function 키워드 대신 화살표를 사용하여 기존의 함수 정의 방식보다 간략하게 함수를 정의할 수 있다.</li>
<li>표현 뿐 아니라 내부 동작도 기존 함수보다 간략하다.</li>
</ul>
<h4 id="함수-정의">함수 정의</h4>
<p>화살표 함수는 함수 선언문으로 정의할 수 없고 함수 표현식으로 정의해야 한다. 호출 방식은 기존 함수와 동일하다.</p>
<h4 id="매개변수-선언">매개변수 선언</h4>
<p>매개변수가 여러 개인 경우 소괄호 () 안에 매개변수를 선언한다.</p>
<h4 id="함수-몸체-정의">함수 몸체 정의</h4>
<ul>
<li>함수 몸체가 하나의 문으로 구성된다면 함수 몸체를 감싸는 중괄호 {}를 생략할 수 있다.</li>
<li>객체 리터럴을 반환하는 경우 객체 리터럴을 소괄호 ()로 감싸주어야 한다.</li>
</ul>
<p>화살표 함수도 즉시 실행 함수로 사용할 수 있다.</p>
<p>화살표 함수도 일급 객체이므로 고차 함수에 인수로 전달할 수 있다.</p>
<blockquote>
<p>화살표 함수는 콜백 함수로서 정의할 때 유용하다. 일반 함수의 기능을 간략화 했으며 this도 편리하게 설계되었다.</p>
</blockquote>
<h3 id="화살표-함수와-일반-함수의-차이">화살표 함수와 일반 함수의 차이</h3>
<ul>
<li><p>화살표 함수는 인스턴스를 생성할 수 없는 non-constructor다.</p>
<ul>
<li>인스턴스를 생성할 수 없으므로 prototype 프로퍼티가 없고 프로토타입도 생성하지 않는다.</li>
</ul>
</li>
<li><p>중복된 매개변수 이름을 선언할 수 없다.</p>
</li>
<li><p>화살표 함수는 함수 자체의 this, arguments, super, new target 바인딩을 갖지 않는다.</p>
</li>
</ul>
<h3 id="this">this</h3>
<p>화살표 함수의 this는 일반 함수의 this와 다르게 동작한다.</p>
<p>화살표 함수 내부에서 this를 참조하면 상위 스코프의 this를 그대로 참조한다. (lexical this)</p>
<p>만약 화살표 함수와 화살표 함수가 중첩되어 있다면 상위 화살표 함수에도 this 바인딩이 없으므로 스코프 체인 상에서 가장 가까운 화살표 함수가 아닌 함수의 this를 참조한다.</p>
<p>프로퍼티에 할당한 화살표 함수도 스코프 체인 상에서 가장 가까운 상위 함수 중에서 화살표 함수가 아닌 함수의 this를 참조한다.</p>
<pre><code class="language-javascript">// Bad
const person = {
    name: 'Lee'.
    sayHi: () =&gt; console.log(`Hi ${this.name}`)
};

person.sayHi(); // Hi

// Good
const person = {
    name: 'Lee',
    sayHi() {
        console.log(`Hi ${this.name}`);
    }
};

person.sayHi(); // Hi Lee</code></pre>
<p>일반 메서드를 화살표 함수로 정의하면 메서드를 호출한 객체를 가리키는 것이 아닌 전역 객체를 가리키므로 ES6 메서드 축약 표현으로 정의한 ES6 메서드를 사용하는 것이 좋다.</p>
<h3 id="super">super</h3>
<p>화살표 함수는 함수 자체의 super 바인딩을 갖지 않는다. 따라서 화살표 함수 내부에서 super를 참조하면 this와 마찬가지로 상위 스코프의 super를 참조한다.</p>
<pre><code class="language-javascript">class Base {
    constructor(name) {
        this.name = name;
    }

    sayHi() {
        return `Hi ${this.name}`;
    }
}

class Derived extends Base {
    // 화살표 함수의 super는 상위 스코프인 constructor의 super를 가리킨다.
    sayHi = () =&gt; `${super.sayHi()} how are you doing?`;
}

const derived = new Derived('Lee');
console.log(derived.sayHi()); // Hi! Lee how are you doing?</code></pre>
<p>super는 내부 슬롯 [[HomeObject]]를 갖는 ES6 메서드 내에서만 사용할 수 있는 키워드다. sayHi 클래스 필드에 할당한 화살표 함수는 ES6 메서드는 아니지만 함수 자체의 super 바인딩을 갖지 않으므로 super를 참조해도 에러가 발생하지 않고 this와 마찬가지로 클래스 필드에 할당한 화살표 함수 내부에서 super를 참조하면 constructor 내부의 super 바인딩을 참조한다. 위 예제의 경우 Derived 클래스의 constructor는 생략 되었지만 암묵적으로 constructor가 생성된다.</p>
<h3 id="arguments">arguments</h3>
<p>화살표 함수는 함수 자체의 arguments 바인딩을 갖지 않는다. 따라서 화살표 함수 내부에서 arguments를 참조하면 this와 마찬가지로 상위 스코프의 arguments를 참조한다.</p>
<p>따라서 화살표 함수로 가변 인자 함수를 구현해야 할 때는 반드시 Rest 파라미터를 사용해야 한다.</p>
<h3 id="rest-파라미터">rest 파라미터</h3>
<ul>
<li>함수에 전달된 인수들의 목록을 배열로 전달받는다.</li>
<li>일반 매개변수와 Rest 파라미터는 함께 사용할 수 있다. 이때 함수에 전달된 인수들은 매개변수와 Rest 파라미터에 순차적으로 할당된다.</li>
<li>rest 파라미터는 이름 그대로 먼저 선언된 매개변수에 할당된 인수를 제외한 나머지 인수들로 구성된 배열이 할당된다. 따라서 Rest 파라미터는 반드시 마지막 파라미터이어야 한다.</li>
<li>rest 파라미터는 단 하나만 선언할 수 있다.</li>
<li>rest 파라미터는 함수 정의 시 선언한 매개변수 개수를 나타내는 함수 객체의 length 프로퍼티에 영향을 주지 않는다.</li>
</ul>