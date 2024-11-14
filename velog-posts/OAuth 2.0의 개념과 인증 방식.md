<p>이번 프로젝트에서 로그인 기능을 OAuth 2.0 기반 카카오 로그인으로 구현하기로 하면서 OAuth에 대한 개념과 동작 원리 등을 찾아보았다.</p>
<h3 id="oauth란">OAuth란?</h3>
<p>OAuth는 인터넷 사용자들이 비밀번호를 제공하지 않고 다른 웹 사이트 상의 자신들의 정보에 대해
웹 사이트나 애플리케이션의 접근 권한을 부여할 수 있는 공통적인 수단으로서 사용되는 접근 위임을 위한 개방형 표준으로, 앱을 사용할 때 사용자가 해당 어플리케이션에 ID,PW 등의 정보를 제공하지 않고 신뢰할 수 있는 외부 어플리케이션의 Open API에 로그인하여 해당 어플의 인증 과정을 처리해주는 방식이다.</p>
<p>OAuth 주요 용어는 다음과 같다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/32bb8274-cb3d-4d51-924d-b5bf1944b4ea/image.png" /></p>
<p>OAuth의 구성요소는 다음과 같다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/b3bdd684-3274-482d-a103-ec35abd3d4ff/image.png" /></p>
<p>OAuth 2.0에서는 4가지 방식을 구현하고 있는데,</p>
<ol>
<li>Authorization Code Grant│ 권한 부여 승인 코드 방식</li>
<li>Implicit Grant │ 암묵적 승인 방식</li>
<li>Resource Owner Password Credentials Grant │ 자원 소유자 자격증명 승인 방식</li>
<li>Client Credentials Grant │클라이언트 자격증명 승인 방식</li>
</ol>
<p>이 존재한다.</p>
<h3 id="권한-부여-승인-코드-방식-authorization-code-grant">권한 부여 승인 코드 방식 (Authorization Code Grant)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/7ec6783c-d666-4e32-8c96-7cf719cf8a3d/image.png" />
권한 부여 승인 코드 방식은 가장 기본적인 방식으로 자체 생성한 Authorization Code를 전달하는 방식으로 많이 쓰인다.</p>
<h3 id="동작-방식">동작 방식</h3>
<ul>
<li>사용자가 사용 요청을 하면 클라이언트에서 권한 서버로 권한 부여에 대한 승인 코드를 요청한다. </li>
<li>승인 코드를 전달받으면 이를 사용하여 Access Token을 요청한다.</li>
<li>Access Token과 Refresh Token을 권한 서버로 부터 전달 받으면 Access Token을 사용해 서버에 권한이 있는 사용자임을 전달함과 동시에 필요한 자원을 요청한다.</li>
<li>클라이언트에서 서버로부터 요청한 자원을 전달받아 사용자에게 반환한다.</li>
</ul>
<p>권한 서버에서 제공하는 client_id와 redirect_URL을 포함하여 response_type을 코드로 지정해 요청하면 권한 서버에서 제공하는 로그인 페이지를 띄워준다. 로그인을 하게 되면 요청 시 전달받은 redirect_url로 권한 코드를 전달하고 이는 Access Token으로 변환되어 서버에 response를 할 수 있게 된다</p>
<h3 id="암묵적-승인-방식-implicit-grant">암묵적 승인 방식 (implicit Grant)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/b732cae9-d974-4c74-9bee-bc0334cb2f2d/image.png" />
암묵적 승인 방식은 자격증명을 안전하게 저장하기 힘든 클라이언트에게 최적화된 방식이다.</p>
<ul>
<li>권한 부여 승인 코드를 생략하고 바로 Access Token이 발급된다.</li>
<li>대신 토큰의 만료기간을 짧게 설정하여 누출의 위험을 줄일 필요가 있다.</li>
<li>Refresh Token 사용이 불가능한 방식이다.</li>
<li>절차가 간소화 되어 응답성과 효율성은 높아지지만 Access Token이 URL로 전달되는 단점이 존재한다.</li>
</ul>
<h3 id="자원-소유자-자격증명-승인-방식-resource-owner-password-credentials-grant">자원 소유자 자격증명 승인 방식 (Resource Owner Password Credentials Grant)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/b5b44617-f79d-4235-9ea7-89e0838a6071/image.png" /></p>
<p>자원 소유자 자격증명 승인 방식은 username, password로 Access Token을 받는 방식이다.</p>
<ul>
<li>권한 부여 승인 코드가 생략된다.</li>
<li>클라이언트가 타사의 외부 프로그램일 경우에는 이 방식을 적용하면 안되며, 자사의 서비스 어플리케이션일 경우에만 적용 가능하다.</li>
<li>Refresh Token의 사용이 가능하다.</li>
</ul>
<h3 id="클라이언트-자격증명-승인-방식-client-credentials-grant">클라이언트 자격증명 승인 방식 (Client Credentials Grant)</h3>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/219b4920-915b-48d1-9d0f-e50efc3829c1/image.png" />
클라이언트 자격증명 승인 방식은 클라이언트의 자격증명만으로 Access Token을 획득하는 방식이다.</p>
<ul>
<li>가장 간단한 방식으로 자신이 관리하는 서버 혹은 권한 서버에 해당 클라이언트의 제한된 리소스 접근 권한이 있는 경우 사용된다.</li>
<li>Refresh Token은 사용할 수 없다.</li>
</ul>
<h3 id="jwt와-oauth의-차이">JWT와 OAuth의 차이</h3>
<p>JWT는 토큰의 종류이고, OAuth는 토큰을 발급하고 인증하는 오픈 스탠다드 프로토콜이다.</p>
<p>JWT는 주로 상태를 유지하지 않는 REST API에서 사용자 인증을 위해 사용된다. 예를 들어, 사용자가 로그인하면 서버는 JWT를 발급하고, 사용자는 이후의 요청에 이 토큰을 포함시켜 서버에 제출함으로써 인증 과정을 거친다. JWT는 클라이언트 측에서 토큰을 저장하고 관리할 수 있기 때문에 주로 간단하고 빠른 인증이 필요할 때 유용하다.</p>
<p>OAuth 2.0은 Google, Facebook과 같은 대형 플랫폼에서 제3자 애플리케이션에 대한 접근 권한을 관리하기 위해 사용된다. 사용자는 이러한 서비스의 로그인 페이지를 통해 인증하고, 애플리케이션은 사용자의 동의를 받아 특정 데이터에 접근할 수 있는 권한을 얻는다. 따라서 사용자의 데이터 접근 권한을 안전하게 관리할 때 적합하다.</p>
<p>다음 블로그에서는 OAuth의 Authorization Code Grant 방식을 사용한 카카오 로그인 기능을 프로젝트에 연동하면서 만났던 오류와 구현 과정을 다뤄보겠다.</p>
<p>[출처] OAuth 2.0 동작 방식의 이해|작성자 MDS인텔리전스</p>