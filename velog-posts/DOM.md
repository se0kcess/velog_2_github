<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/13747dcf-c3e3-49f2-ba5b-25f80b677969/image.png" /></p>
<h3 id="dom">DOM</h3>
<p>HTML 문서의 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API, 즉 프로퍼티와 메서드를 제공하는 트리 자료구조이다.</p>
<h3 id="html-요소">HTML 요소</h3>
<p>HTML 요소는 HTML 문서를 구성하는 개별적인 요소이다.
<img alt="" src="https://velog.velcdn.com/images/se0kcess/post/34a0ac23-3aa5-479a-982e-bd0f4c222b2b/image.png" /></p>
<p><strong>HTML 요소는 렌더링 엔진에 의해 파싱되어 DOM을 구성하는 요소 노드 객체로 변환</strong></p>
<ul>
<li>HTML 요소의 어트리뷰트 -&gt; 어트리뷰트 노드</li>
<li>HTML 요소의 텍스트 콘텐츠 -&gt; 텍스트 노드</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/e7505de5-4cf5-44ee-8a2b-0ab9635542cd/image.png" /></p>
<p>HTML 요소 간에 중첩 관계에 의해 계층적인 부자 관계 형성 -&gt; HTML 요소를 객체화한 모든 노드 객체들을 트리 자료구조로 구성</p>
<h3 id="트리-자료구조">트리 자료구조</h3>
<ul>
<li>노드들의 계층 구조로 이루어진다.</li>
<li>부모 노드와 자식 노드로 구성되어 노드 간의 계층적 구조를 표현하는 비선형 자료구조</li>
<li>최상위 노드(루트 노드)에서 시작</li>
</ul>
<p>루트 노드 (최상위 노드, 부모 노드 x)
리프 노드 (말단 노드, 자식 노드가 없는 노드)</p>
<h3 id="dom-dom-트리">DOM (DOM 트리)</h3>
<p>노드 객체들로 구성된 트리 자료구조</p>
<h3 id="노드-타입">노드 타입</h3>
<ul>
<li>문서 노드 : DOM 트리의 최상위에 존재하는 루트 노드로서 document 객체를 가리킨다.<ul>
<li>DOM 트리의 루트 노드이므로 DOM 트리의 노드들에 접근하기 위한 진입점 역할을 담당</li>
<li>요소, 어트리뷰트, 텍스트 노드에 접근하려면 문서 노드를 통해야 한다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>document 객체 : 브라우저가 렌더링한 HTML 문서 전체를 가리키는 객체, window의 document 프로퍼티에 바인딩</p>
</blockquote>
<ul>
<li><p>요소 노드 : HTML 요소를 가리키는 객체이다</p>
<ul>
<li>HTML 요소 간의 중첩에 의해 부자 관계를 가지며 부자 관계를 통해 정보를 구조화한다.</li>
<li>문서의 구조 표현</li>
</ul>
</li>
<li><p>어트리뷰트 노드 : HTML 요소의 어트리뷰트를 가리키는 객체이다.</p>
<ul>
<li>어트리뷰트가 지정된 HTML 요소의 요소 노드와 연결되어 있다.</li>
<li>부모 노드와 연결되어 있지 않고 요소 노드에만 연결</li>
<li>어트리뷰트 노드에 접근하여 어트리뷰트를 참조하거나 변경하려면 요소 노드에 먼저 접근</li>
</ul>
</li>
<li><p>텍스트 노드 : HTML의 텍스트를 가리키는 객체이다.</p>
<ul>
<li>요소 노드의 자식 노드이며 자식을 가질 수 없는 리프 노드이다.</li>
<li>DOM 트리의 최종단이다.</li>
<li>텍스트 노드에 접근하려면 부모 노드인 요소 노드에 접근해야 한다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>DOM을 구성하는 노드 객체는 ECMAScript 사양에 정의된 표준 빌트인 객체가 아니라 브라우저 환경에서 추가적으로 제공하는 호스트 객체이다.</p>
</blockquote>
<p>하지만 노드 객체도 자바스크립트 객체이므로 프로토타입에 의한 상속 구조를 갖는다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/4ac762cf-e7ed-4620-9c1c-44d8de03ab79/image.png" /></p>
<h3 id="노드-객체의-특성">노드 객체의 특성</h3>
<ul>
<li>모든 노드 객체가 공통으로 갖는 기능도 있고 노드 타입에 따라 고유한 기능도 있다.</li>
<li>이벤트에 관련된 기능은 EventTarget 인터페이스가 제공</li>
<li>모든 노드 객체는 트리 자료구조의 노드로서 공통적으로 트리 탐색 기능이나 노드 정보 제공 기능이 필요하다. -&gt; Node 인터페이스가 제공</li>
<li>HTML 요소가 갖는 공통적인 기능은 HTMLElement 인터페이스가 제공</li>
</ul>
<blockquote>
<p>노드 객체는 공통 기능은 프로토타입 체인 상위에, 개별적인 고유 기능일수록 프로토타입 체인 하위에 프로토타입 체인 구축하여 상속 구조를 갖는다.</p>
</blockquote>
<p>DOM은 HTML 문서의 계층적 구조와 정보를 표현하며 노드 타입에 따라 필요한 기능을 프로퍼티와 메서드의 집합인 DOM API로 제공한다.</p>
<p>DOM API를 통해 HTML의 구조나 내용 또는 스타일을 동적으로 조작할 수 있다.</p>
<h2 id="요소-노드-취득">요소 노드 취득</h2>
<h3 id="id를-이용한-요소-노드-취득-documentprototypegetelementbyid">id를 이용한 요소 노드 취득 (Document.prototype.getElementByID)</h3>
<ul>
<li>id 값은 HTML 문서 내에서 유일한 값이며 class 어트리뷰트와 달리 공백 문자로 구분하여 여러 개의 값을 가질 수 없다.</li>
<li>HTML 요소 내에 중복된 id 값을 갖는 요소가 여러 개 존재할 가능성이 있다.</li>
<li>인수로 전달된 id 값을 갖는 첫 번째 요소 노드만 반환한다.</li>
<li>인수로 전달된 id 값을 갖는 HTML 요소가 존재하지 않은 경우 null 반환</li>
<li>HTML 요소에 id 어트리뷰트를 부여하면 id 값과 동일한 이름의 전역 변수가 암묵적으로 선언되고 해당 노드 객체가 할당되는 부수 효과 발생</li>
<li>id 값과 동일한 이름의 전역 변수가 이미 선언되어 있으면 이 전역 변수에 노드 객체가 재할당되지 않음</li>
</ul>
<h3 id="태그-이름을-이용한-요소-취득-getelementsbytagname">태그 이름을 이용한 요소 취득 (getElementsByTagName)</h3>
<ul>
<li>인수로 전달한 태그 이름을 갖는 모든 요소 노드를 탐색하여 반환</li>
<li>여러 개의 요소 노드 객체를 갖는 DOM 컬렉션 객체인 HTMLCollection 객체 반환</li>
<li>반환하는 HTMLCollection 객체는 유사 배열 객체이자 이터러블</li>
<li>인수로 전달된 태그 이름을 갖는 요소가 존재하지 않는 경우 getElementsByTagName 메서드는 빈 HTMLCollection 객체를 반환한다.</li>
</ul>
<h3 id="class를-이용한-요소-노드-취득-getelementsbyclassname">class를 이용한 요소 노드 취득 (getElementsByClassName)</h3>
<ul>
<li>인수로 전달한 class 어트리뷰트 값을 갖는 모든 요소 노드들을 탐색하여 반환한다.</li>
<li>인수로 전달할 class 값은 공백으로 구분하여 여러 개의 class를 지정할 수 있다.</li>
<li>여러 개의 요소 노드 객체를 갖는 HTMLCollection 객체를 반환한다.</li>
<li>인수로 전달된 class 값을 갖는 요소가 존재하지 않는 경우 getElementsByClassName 메서드는 빈 HTMLCollection 객체를 반환한다.</li>
</ul>
<h3 id="css-선택자를-이용한-요소-노드-취득">CSS 선택자를 이용한 요소 노드 취득</h3>
<ul>
<li>스타일을 적용하고자 하는 HTML 요소를 특정할 때 사용하는 문법</li>
<li>인수로 전달할 CSS 선택자를 만족시키는 하나의 요소 노드를 탐색하여 반환</li>
<li>요소 노드가 여러 개인 경우 첫 번째 요소 노드만 반환</li>
<li>요소 노드가 존재하지 않는 경우 null 반환</li>
<li>CSS 선택자가 문법에 맞지 않는 경우 DOMException 에러 발생</li>
</ul>
<p><strong>querySelectorAll 메서드는 인수로 전달한 CSS 선택자를 만족시키는 모든 요소 노드를 탐색하여 반환한다.</strong></p>
<ul>
<li>여러개의 요소 노드 객체를 갖는 NodeList 객체를 반환한다. Node 객체는 유사 배열 객체이면서 이터러블이다.</li>
<li>getElementById, getElementsBy*** 메서드보다 느리지만 구체적인 조건으로 요소 노드를 취득할 수 있고 일관된 방식으로 취득할 수 있다.</li>
</ul>
<h3 id="elementprototypematches">Element.prototype.matches</h3>
<ul>
<li>인수로 전달한 CSS 선택자를 통해 특정 요소 노드를 취득할 수 있는지 확인한다.</li>
<li>이벤트 위임 사용 시 유용</li>
</ul>
<h3 id="htmlcollection과-nodelist">HTMLCollection과 NodeList</h3>
<ul>
<li>DOM API가 여러 개의 결과값을 반환하기 위한 DOM 컬렉션 객체로, 모두 유사 배열이면서 이터러블이다.</li>
<li>for...of 문으로 순회할 수 있으며 스프레드 문법을 사용하여 간단한 배열로 변경 가능하다.</li>
<li>노드 객체의 상태 변화를 실시간으로 반영하는 살아있는 객체이다.</li>
</ul>
<h3 id="htmlcollection">HTMLCollection</h3>
<ul>
<li>실시간으로 노드 객체의 상태 변경을 반영하여 요소를 제거할 수 있기 때문에 for문으로 순회하면서 상태 변경 시 주의해야 한다.</li>
<li>for문 역방향 순회, while문 사용 등으로 회피 가능 + 고차 함수</li>
</ul>
<h3 id="nodelist">NodeList</h3>
<ul>
<li>querySelectorAll 메서드를 사용하여 실시간 노드 객체의 상태변경을 반영하지 않는 NodeList 객체 사용</li>
<li>childNodes 프로퍼티가 반환하는 NodeList 객체는 실시간으로 노드 객체의 상태 변경을 반영하는 live 객체이므로 동작의 주의가 필요하다.</li>
</ul>
<blockquote>
<p>노드 객체의 상태 변경과 상관없이 안전하게 DOM 컬렉션을 사용하려면 HTMLCollection이나 NodeList 객체를 배열로 변환하여 사용하는 것을 권장한다.</p>
</blockquote>
<h3 id="노드-탐색">노드 탐색</h3>
<p>DOM 트리 상의 노드를 탐색할 수 있도록 Node, Element 인터페이스는 트리 탐색 프로퍼티를 제공한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/d14ae3ce-c95a-4655-bdc9-55a9aa0fbade/image.png" /></p>
<p>노드 탐색 프로퍼티는 모드 접근자 프로퍼티다.
단 setter 없이 getter 만 존재하여 참조만 가능한 읽기 전용 접근자 프로퍼티다.
읽기 전용 접근자 프로퍼티에 값을 할당하면 아무런 에러없이 무시된다.</p>
<h3 id="공백-텍스트-노드">공백 텍스트 노드</h3>
<ul>
<li>HTML 요소 사이의 스페이스, 탭, 줄바꿈 등의 공백 문자는 텍스트 노드를 생성한다.</li>
<li>공백 문자는 공백 텍스트 노드를 생성한다</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/3b853a54-a3fd-4be1-b012-539b0fb61914/image.png" /></p>
<h3 id="자식-노드-탐색">자식 노드 탐색</h3>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/06d3f5df-3e40-4bf5-98d9-bdb8ea6f2ade/image.png" />
<img alt="" src="https://velog.velcdn.com/images/se0kcess/post/0e22ec1e-4e64-43b4-8cb1-e12714aabee0/image.png" /></p>
<ul>
<li>Node.porotype.hasChildNodes : 자식 노드가 존재하는지 확인한다. 불리언 값을 반환한다. 리프 노드라면 텍스트 노드를 포함한다.</li>
<li>자식 노드 중에 텍스트 노드가 아닌 요소 노드가 존재하는지 확인하려면 children.length 또는 Element 인터페이스의 childElementCount 프로퍼티를 사용한다.</li>
</ul>
<h3 id="부모-노드-탐색">부모 노드 탐색</h3>
<ul>
<li>Node.prototype.parentNode : 부모 노드를 탐색한다.</li>
<li>텍스트 노드는 리프 노드이므로 부모 노드가 텍스트 노드인 경우는 없다.</li>
</ul>
<h3 id="형제-노드-탐색">형제 노드 탐색</h3>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/5faab031-8832-40cd-a8c1-e338a35709a4/image.png" />
<img alt="" src="https://velog.velcdn.com/images/se0kcess/post/3ad7c0cb-474f-4740-acb2-da43a20ce060/image.png" /></p>
<h3 id="노드-정보-취득">노드 정보 취득</h3>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/463166ac-cced-4bca-b3a8-db949997df5c/image.png" /></p>
<h3 id="nodevalue">nodeValue</h3>
<p>setter와 getter 모두 존재하는 접근자 프로퍼티이므로 참조와 할당 모두 가능하다.</p>
<p>노드 객체의 nodeValue 프로퍼티를 참조하면 노드 객체의 값(텍스트 노드의 텍스트)을 반환한다. 따라서 텍스트 노드가 아닌 노드의 프로퍼티를 참조하면 null을 반환한다.</p>
<p>텍스트 노드의 nodeValue 프로퍼티에 값을 할당하면 텍스트를 변경할 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/240b6a7f-0e9a-45d0-873c-a927da3e91d9/image.png" /></p>
<h3 id="textcontent">textContent</h3>
<p>setter와 getter 모두 존재하는 접근자 프로퍼티로서 요소 노드의 텍스트와 모든 자손 노드의 텍스트를 모두 취득하거나 변경한다.</p>
<p>요소 노드의 textContent 프로퍼티를 참조하면 요소 노드의 콘텐츠 영역 내의 텍스트를 모두 반환한다.</p>
<h3 id="dom-조작">DOM 조작</h3>
<p>새로운 노드를 생성하여 DOM에 추가하거나 기존 노드를 삭제 또는 교체하는 것
DOM 조작에 의해 새로운 노드가 추가되거나 삭제되면 리플로우와 리페인트가 발생한다.</p>
<h3 id="innerhtml">innerHTML</h3>
<p>setter와 getter 모두 존재하는 접근자 프로퍼티로서 요소 노드의 HTML 마크업을 취득하거나 변경한다.</p>
<ul>
<li>getter: 마크업이 포함된 문자열을 문자열 그대로 (변환없이) 반환</li>
<li>setter: 요소 노드의 innerHTML 프로퍼티에 문자열을 할당하면 마크업이 파싱되어, 요소 노드의 자식 노드로  DOM에 반환</li>
</ul>
<h3 id="장점">장점</h3>
<p>구현이 간단하고 직관적이다.</p>
<h3 id="단점">단점</h3>
<ul>
<li>크로스 사이트 스크립팅 공격에 취약하다.</li>
<li>요소 노드의 innerHTML 프로퍼티에 HTML 마크업 문자열 할당하면 요소 노드의 모든 자식 노드를 제거하고 할당한 HTML 마크업 문자열을 파싱하여 DOM을 변경한다.</li>
<li>새로운 요소 삽입 시 삽입될 위치를 지정하지 못한다.</li>
</ul>
<h3 id="insertadjacenthtml">insertAdjacentHTML</h3>
<ul>
<li>기존 요소 제거하지 않으면서 위치 지정해 새로운 요소 삽입한다.
innerHTML 프로퍼티보다 효율적이고 빠르지만 XSS 공격에 취약하다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/22519020-2aad-47bb-90e7-e33eb4df72a7/image.png" /></p>
<h3 id="노드-생성과-추가">노드 생성과 추가</h3>
<h3 id="documentprototypecreateelementtagname-메서드">Document.prototype.createElement(tagName) 메서드</h3>
<p>요소 노드를 생성하여 반환한다</p>
<ul>
<li>생성된 요소 노드는 아무런 자식 노드가 없다</li>
<li>tagName: 태그 이름 나타내는 문자열을 인수로 전달한다.</li>
</ul>
<h3 id="documentprototypecreatetextnodetext-메서드">Document.prototype.createTextNode(text) 메서드</h3>
<ul>
<li>텍스트 노드를 생성하여 반환한다.</li>
<li>text: 텍스트 노드의 값으로 사용할 문자열을 인수로 전달</li>
</ul>
<h3 id="nodeprototypeappendchildchildnode-메서드">Node.prototype.appendChild(childNode) 메서드</h3>
<ul>
<li>childNode를 메서드를 호출한 노드의 마지막 자식 노드로 추가</li>
<li>textContent 프로퍼티 사용하는 것이 더 간편하다.</li>
</ul>
<h3 id="nodeprototypeappendchild-메서드">Node.prototype.appendChild 메서드</h3>
<ul>
<li>단 하나의 요소 노드 생성하여 DOM에 한번 추가하면 DOM은 한 번 변경된다.</li>
<li>리플로우와 리페인트가 1번 실행된다.</li>
</ul>
<hr />
<h3 id="복수의-노드-생성과-추가">복수의 노드 생성과 추가</h3>
<p>배열의 forEach 메서드를 이용한다.
DOM 변경하는 것은 높은 비용이 드는 처리이므로 가급적 횟수 줄이는 것이 성능에 유리하다.</p>
<h3 id="컨테이너-요소-사용">컨테이너 요소 사용</h3>
<p>DOM을 한 번만 변경하므로 성능에 유리하지만 불필요한 컨테이너 요소 추가되는 부작용이 발생한다.</p>
<h3 id="documentfragment-노드-사용">DocumentFragment 노드 사용</h3>
<p>자식 노드들의 부모 노드로서 별도의 sub DOM을 구성하여 기존 DOM에 추가하기 위한 용도로 사용한다.</p>
<hr />
<h3 id="노드-삽입">노드 삽입</h3>
<h3 id="nodeprototypeappendchild-메서드-1">Node.prototype.appendChild 메서드</h3>
<p>항상 마지막 자식 노드로 추가한다.</p>
<h3 id="nodeprototypeinsertbeforenewnode-childnode-메서드">Node.prototype.insertBefore(newNode, childNode) 메서드</h3>
<ul>
<li>첫 번째로 전달받은 노드를 두 번째 인수로 전달받은 노드 앞에 삽입한다.</li>
<li>두 번째 인수로 전달받은 노드는 반드시 insertBefore 메서드를 호출한 노드의 자식 노드여야 한다.</li>
<li>두 번째 인수로 전달받은 노드가 null이면 첫 번째 인수로 전달받은 노드를 마지막 자식 노드로 추가한다.</li>
</ul>
<hr />
<h3 id="노드-이동">노드 이동</h3>
<p>DOM에 이미 존재하는 노드를 appendChild/insertBefore 메서드를 사용하여 DOM에 다시 추가하면, 현재 위치에서 노드를 제거하고 새로운 위치에 노드를 추가한다.</p>
<h3 id="노드-복사">노드 복사</h3>
<h3 id="nodeprototypeclonenodedeep-true--false-메서드">Node.prototype.cloneNode([deep: true | false]) 메서드</h3>
<ul>
<li>노드의 사본을 생성하여 반환한다.</li>
<li>deep에 true로 인수 전달 시, 노드 깊은 복사하여 모든 자손 노드 포함된 사본 생성한다.</li>
<li>false로 인수 전달 시, 노드 얕은 복사 하여 노드 자신만의 사본을 생성한다.</li>
<li>얕은 복사로 생성된 요소 노드는 자손 노드를 복사하지 않으므로 텍스트 노드도 없다.</li>
</ul>
<h3 id="노드-교체">노드 교체</h3>
<h3 id="nodeprototypereplacechildnewchild-oldchild-메서드">Node.prototype.replaceChild(newChild, oldChild) 메서드</h3>
<ul>
<li>자신을 호출한 노드의 자식 노드인 oldChild를 newChild 노드로 교체한다.</li>
<li>oldChild 노드는 DOM에서 제거된다.</li>
</ul>
<hr />
<h3 id="노드-삭제">노드 삭제</h3>
<h3 id="nodeprototyperemovechildchild-메서드">Node.prototype.removeChild(child) 메서드</h3>
<h3 id="어트리뷰트-노드">어트리뷰트 노드</h3>
<p>HTML 문서가 파싱될 때 HTML 요소의 어트리뷰트는 어트리뷰트 노드로 변환되어 요소 노드와 연결된다.</p>
<p>모든 어트리뷰트 노드의 참조는 유사 배열 객체, 이터러블인 NamedNodeMap 객체에 담겨서
요소 노드의 attritbutes 프로퍼티에 저장된다.</p>
<h3 id="elementprototypeattributes-프로퍼티">Element.prototype.attributes 프로퍼티</h3>
<ul>
<li>요소 노드의 모든 어트리뷰트 노드 취득이 가능하다.</li>
<li>getter만 존재하는 읽기 전용 접근자 프로퍼티이다.</li>
<li>요소 노드의 모든 어트리뷰트 노드의 참조가 담긴 NamedNodeMap 객체를 반환한다.</li>
</ul>
<h3 id="html-어트리뷰트-조작">HTML 어트리뷰트 조작</h3>
<p><strong>Element.prototype.getAttribute/setAttribute 메서드</strong></p>
<ul>
<li>요소 노드에서 메서드를 통해 직접 HTML 어트리뷰트 값을 취득하거나 변경 가능하므로 편리하다.</li>
</ul>
<p><strong>Element.prototype.getAttribute(attributeName) 메서드</strong></p>
<ul>
<li>HTML 어트리뷰트 값 참조</li>
</ul>
<p><strong>Element.prototype.setAttribute(attributeName, attributeValue) 메서드</strong></p>
<ul>
<li>HTML 어트리뷰트 값 변경</li>
</ul>
<p><strong>Element.prototytpe.hasAttribute(attributeName) 메서드</strong></p>
<ul>
<li>특정 HTML 어트리뷰트 존재하는지 확인</li>
</ul>
<p><strong>Element.prototype.removeAttribute(attributeName) 메서드</strong></p>
<ul>
<li>특정 HTML 어트리뷰트 삭제</li>
</ul>
<hr />
<h3 id="요소의-상태-관리">요소의 상태 관리</h3>
<ul>
<li>요소 노드의 초기 상태는 어트리뷰트 노드가 관리</li>
<li>요소 노드의 최신 상태는 DOM 프로퍼티가 관리</li>
</ul>
<h3 id="어트리뷰트-노드-1">어트리뷰트 노드</h3>
<ul>
<li>HTML 어트리뷰트로 지정한 HTML 요소의 초기 상태는 어트리뷰트 노드에서 관리한다.</li>
<li>HTML 요소 초기 상태를 그대로 유지한다.</li>
<li>초기 상태 값 취득하거나 변경하기 위해 getAttribute/setAttribute 메서드를 사용한다.</li>
</ul>
<h3 id="dom-프로퍼티">DOM 프로퍼티</h3>
<p>사용자가 입력한 최신 상태는 HTML 어트리뷰트에 대응하는 요소 노드의 DOM 프로퍼티가 관리한다.</p>
<ul>
<li>사용자의 입력에 의한 상태 변화에 반응하여 언제나 최신 상태를 유지한다.</li>
<li>HTML 요소에 지정한 어트리뷰트 값에는 어떠한 영향도 주지 않는다.</li>
<li>모든 DOM 프로퍼티가 사용자의 입력에 의해 변경되 최신 상태 관리하는 것은 아니다.</li>
</ul>
<h3 id="html-어트리뷰트와-dom-프로퍼티의-대응-관계">HTML 어트리뷰트와 DOM 프로퍼티의 대응 관계</h3>
<p>대부분의 HTML 어트리뷰트는 HTML 어트리뷰트 이름과 동일한 DOM 프로퍼티와 1:1로 대응하지만 언제나 1:1로 대응하는 것은 아니며 HTML 어트리뷰트 이름과 DOM 프로퍼티 키가 반드시 일치하는 것도 아니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/161f4a34-6e1b-40bd-a6c5-3b8f331934be/image.png" /></p>
<h3 id="dom-프로퍼티-값의-타입">DOM 프로퍼티 값의 타입</h3>
<p>getAttribute 메서드로 취득한 어트리뷰트 값은 항상 문자열 타입이다.
DOM 프로퍼티로 취득한 최신 상태 값은 문자열 타입이 아닐 수 있다.</p>
<h3 id="data-어트리뷰트와-dataset-프로퍼티">data 어트리뷰트와 dataset 프로퍼티</h3>
<p>HTML 요소에 정의한 사용자 정의 어트리뷰트와 JS 간에 데이터 교환 가능하다.</p>
<ul>
<li>data 어트리뷰트 값은 HTMLElement.dataset 프로퍼티로 취득 가능하다.</li>
<li>dataset 프로퍼티는 HTML 요소의 모든 data 어트리뷰트 정보 제공하는 DOMStringMap 객체를 반환한다.</li>
<li>DOMStringMap 객체에 data- 접두사 다음에 카멜 케이스로 변환한 프로퍼티 가지고 있다.</li>
<li>반대로 동적으로 HTML 요소에 data 어트리뷰트 추가하면 케밥 케이스로 자동 변경되어 추가된다.</li>
</ul>
<hr />
<h2 id="스타일">스타일</h2>
<h3 id="인라인-스타일-조작">인라인 스타일 조작</h3>
<p>HTMLElement.prototype.style 프로퍼티로 setter, getter 모두 존재하는 접근자 프로퍼티이다.
요소 노드의 인라인 스타일을 취득하거나 추가/변경이 가능하다.</p>
<p>style 프로퍼티 참조 시 CSSStyleDeclaration 타입의 객체를 반환한다.</p>
<ul>
<li>CSS 프로퍼티는 케밥 케이스를 따른다.</li>
<li>CSSStyleDeclaration 객체의 프로퍼티는 카멜 케이스를 따른다.</li>
</ul>
<h3 id="클래스-조작">클래스 조작</h3>
<h3 id="classname">className</h3>
<ul>
<li>Element.prototype.className 프로퍼티<ul>
<li>setter, getter 모두 존재하는 접근자 프로퍼티        </li>
<li>HTML 요소의 class 어트리뷰트 값을 취득하거나 변경한다.</li>
</ul>
</li>
</ul>
<h3 id="classlist">classList</h3>
<ul>
<li>Element.prototype.classList 프로퍼티<ul>
<li>class 어트리뷰트의 정보를 담은 DOMTokenList 객체를 반환한다.</li>
<li>DOMTokenList; 노드 객체의 상태 변화를 실시간으로 반영하는 live 객체, class 어트리뷰트의 정보를 나타내는 컬렉션 객체로서 유사 배열이자 이러터블이다.<ul>
<li>add(...className): 인수로 전달한 1개 이상의 문자열을 class 어트리뷰트 값으로 추가한다.</li>
<li>remove(...className): 인수로 전달한 1개 이상의 문자열과 일치하는 클래스를 class 어트리뷰트에서 삭제한다.</li>
<li>item(index): 인수로 전달한 index에 해당하는 클래스를 class 어트리뷰트에서 반환한다.</li>
<li>contains(className): 인수로 전달한 문자열과 일치하는 클래스가 class 어트리뷰트에 포함되어 있는지 확인한다.</li>
<li>replace(oldClassName, newClassName): class 어트리뷰트에서 첫 번째 인수로 전달한 문자열을 두 번째 인수로 전달한 문자열로 변경한다.</li>
<li>toggle(className[, force]): class 어트리뷰트에 인수로 전달한 문자열과 일치하는 클래스가 존재하면 제거하고, 존재하지 않으면 추가한다. / 두 번째 인수로 불리언 값으로 평가되는 조건식 전달 가능하다.
true =&gt; 강제로 첫 번째 인수로 전달받은 문자열 추가, false =&gt; 강제로 제거</li>
</ul>
</li>
</ul>
</li>
</ul>
<h3 id="요소에-적용되어-있는-css-스타일-참조">요소에 적용되어 있는 CSS 스타일 참조</h3>
<ul>
<li>window.getComputedStyle(element, pseudo]) 메서드<ul>
<li>HTML 요소에 적용되어 있는 모든 CSS 스타일을 참조한다.</li>
<li>첫 번째 인수로 전달한 요소 노드에 적용되어 있는 computed 스타일을 CSSStyleDeclaration 객체에 담아 반환한다.</li>
<li>두 번째 인수로 :after, :before 와 같은 pseudo element를 지정하는 문자열 전달이 가능하다.</li>
</ul>
</li>
</ul>