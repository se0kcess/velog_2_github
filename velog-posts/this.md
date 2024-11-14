<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/e1daee85-b051-43ba-b15a-3e7c37f8f904/image.png" />
<strong>메서드가 자신이 속한 객체의 프로퍼티를 참조하려면 먼저 자신이 속한 객체를 가리키는 식별자를 참조할 수 있어야 한다.</strong></p>
<ul>
<li>객체 리터럴 방식으로 생성한 객체의 경우 메서드 내부에서 재귀적으로 참조 가능<pre><code class="language-javascript">const circle = {
// 프로퍼티, 객체 고유의 상태 데이터
radius: 5,
// 메서드: 상태 데이터를 참조하고 조작하는 동작
getDiameter() {
// 이 메서드가 자신이 속한 객체의 프로퍼티나 다른 메서드를 참조하려면
// 자신이 속한 객체인 circle을 참조할 수 있어야 함
return 2 * circle.radius;
}
};
</code></pre>
</li>
</ul>
<p>console.log(circle.getDiameter());</p>
<pre><code>- 객체 리터럴은 circle 변수에 할당되기 직전에 평가됨
- getDiameter 메서드가 호출되는 시점에는 이미 객체 리터럴의 평가가 완료되어 circle 식별자에 생성된 객체가 할당된 이후이므로 메서드 내부에서 circle 식별자를 참조할 수 있음

### this
- 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수
- this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드 참조 가능

&gt;this는 자바스크립트 엔진에 의해 암묵적으로 생성되며 코드 어디서든 참조 가능.
this 바인딩은 함수 호출 방식에 의해 동적으로 결정

### 바인딩
- 식별자와 값을 연결하는 과정
- this 바인딩은 this와 this가 가리킬 객체를 바인딩하는 것

**자바스크립트의 this는 함수가 호출되는 방식에 따라 this에 바인딩될 값, 즉 this 바인딩이 동적으로 결정됨**

### 렉시컬 스코프와 this 바인딩의 결정 시기
함수의 상위 스코프를 결정하는 방식인 렉시컬 스코프는 함수 정의가 평가되어 함수 객체가 생성되는 시점에 상위 스코프를 결정하지만 this 바인딩은 함수 호출 시점에 결정됨

### 함수 호출 방식 this 바인딩
1. 일반 함수 호출
2. 메서드 호출
3. 생성자 함수 호출
4. apply/call/bind 메서드에 의한 간접 호출

### 일반 함수 호출
- 일반적인 함수 호출 시에는 this에 전역 객체가 바인딩 됨
- (strict mode가 적용된 일반 함수 내부의 this에는 undefined가 바인딩됨)
- 콜백함수나 중첩함수의 경우에도 일반 함수로 호출되면 this에 전역 객체가 바인딩 된다.

**메서드 내부의 중첩 함수나 콜백 함수의 this 바인딩을 메서드의 this 바인딩과 일치시키기 위한 방법**
```javascript
var value = 1;

const obj = {
  value: 100,
  foo() {
    // this 바인딩을 변수 that에 할당
    const that = this;

    // 콜백 함수 내부에서 this 대신 that을 참조
    setTimeout(function(){
      console.log(that.value);
    },100);
  }
};

obj.foo();</code></pre><h3 id="메서드-호출">메서드 호출</h3>
<ul>
<li>메서드 내부의 this에는 메서드를 호출한 객체, 메서드를 호출할 때 메서드 이름 앞의 마침표 연산자 앞에 기술한 객체가 바인딩 됨</li>
</ul>
<pre><code class="language-javascript">const person = {
  name: 'Lee',
  getName(){
    // 메서드 내부의 this는 메서드를 호출한 객체에 바인딩
    return this.name;
  }
};

// 메서드 getName을 호출한 객체는 person이다.
console.log(person.getName()); // Lee</code></pre>
<h3 id="생성자-함수-호출">생성자 함수 호출</h3>
<p>생성자 함수 내부의 this에는 생성자 함수가 생성할 인스턴스가 바인딩 됨</p>
<pre><code class="language-javascript">// 생성자 함수
function Circle(radius) {
  // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킴
  this.radius = radius;
  this.getDiameter = function() {
    return 2 * this.radius;
  };
}

// 반지름이 5인 Circle 객체 생성
const circle1 = new Circle(5);
// 반지름이 10인 Circle 객체 생성
const circle2 = new Circle(10);

console.log(circle1.getDiameter()); // 10
console.log(circle2.getDiameter()); // 20</code></pre>
<h3 id="apply-call-bind">apply, call, bind</h3>
<ul>
<li>function.prototype의 메서드인 apply, call, bind를 상속받아 사용</li>
<li>this로 사용할 객체와 인수 리스트를 인수로 전달받아 함수를 호출함</li>
</ul>
<h4 id="apply와-call-메서드의-본질적인-기능--함수-호출">apply와 call 메서드의 본질적인 기능 : 함수 호출</h4>
<ul>
<li>apply 메서드는 호출할 함수의 인수를 배열로 묶어 전달</li>
<li>call 메서드는 호출할 함수의 인수를 쉼표로 구분한 리스트 형식으로 전달</li>
</ul>
<p>arguments 객체와 같은 유사 배열 객체에 배열 메서드를 사용하는 경우 사용</p>
<h4 id="bind-메서드-메서드의-this와-메서드-내부의-중첩함수-또는-콜백-함수의-this가-불일치하는-문제-해결하기-위해-사용">bind 메서드: 메서드의 this와 메서드 내부의 중첩함수 또는 콜백 함수의 this가 불일치하는 문제 해결하기 위해 사용</h4>