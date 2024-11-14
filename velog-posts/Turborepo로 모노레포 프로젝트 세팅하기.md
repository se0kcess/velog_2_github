<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/55d3818e-8138-4b91-9e1a-7fcab46acec4/image.png" /></p>
<h3 id="monorepo">Monorepo</h3>
<p>Monolithic Repositories의 약자로 하나의 프로젝트에서 여러 개의 프로젝트가 가능하도록 구성된 레포지토리 관리 방법이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/se0kcess/post/b97b347c-f32e-4742-a1e7-dcdb85040837/image.png" /></p>
<p>monorepo를 위한 라이브러리로는</p>
<ul>
<li>Yarn berry + workspace</li>
<li>Lerna</li>
<li>Nx</li>
<li>Turborepo</li>
</ul>
<p>와 같은 대표적인 라이브러리가 존재한다.</p>
<p>그 중 turborepo는 Javascript/Typescript를 위한 고성능 빌드 시스템으로 다음과 같은 특징을 가지고 있다.</p>
<h3 id="1-모노레포-관리">1. 모노레포 관리</h3>
<p><strong>워크스페이스 관리</strong>: 여러 프로젝트/패키지를 단일 저장소에서 관리
<strong>의존성 관리</strong>: 워크스페이스 간 의존성을 효율적으로 관리
<strong>병렬 실행:</strong> 여러 태스크를 동시에 실행하여 빌드 시간 단축</p>
<ul>
<li>빌드에 필요한 요소만으로 모노레포의 하위 집합을 생성해 Paas 배포 속도를 높인다.</li>
</ul>
<h3 id="2-캐싱-시스템">2. 캐싱 시스템</h3>
<p><strong>로컬 캐싱</strong>: 이전 빌드 결과를 캐싱하여 재빌드 시간 단축
<strong>원격 캐싱</strong>: 팀원 간 캐시 공유 가능
<strong>증분 빌드</strong>: 변경된 부분만 빌드하여 효율성 증가</p>
<ul>
<li>한 번 빌드된 내용은 캐싱하여 다시 빌드하지 않는다.</li>
<li>콘텐츠를 인식하여 모든 파일을 다시 빌드하는 것이 아닌 변경된 파일만 빌드한다.</li>
</ul>
<h3 id="3-파이프라인-관리">3. 파이프라인 관리</h3>
<ul>
<li><strong>태스크 오케스트레이션</strong>: 빌드, 테스트, 린트 등의 작업을 순서대로 실행</li>
<li><strong>의존성 그래프</strong>: 태스크 간 의존성을 자동으로 분석</li>
<li><strong>병렬 처리</strong>: 독립적인 태스크를 동시에 실행</li>
<li>JSON으로 turborepo를 설정해 사용할 수 있고 빌드 프로필로 빌드 과정을 시각화할 수 있다.</li>
</ul>
<h3 id="장점">장점</h3>
<p>Vercel사에서 운영하는 프로젝트답게 앱은 기본적으로 Next.js(react)로 설정된다. 그외에 Express, Remix, pnpm 등 다양한 기술 스택으로 이루어진 예시도 제공하고 있으므로 필요에 따라 참고할 수 있다.</p>
<p>이번 프로젝트에서 모노레포 방식으로 프론트엔드와 백엔드 작업을 진행해야 했기에 Turborepo를 사용해서 관리하기로 하였다.</p>
<h3 id="폴더-구조">폴더 구조</h3>
<pre><code>my-project/
├── .eslintrc.js    
├── .eslintignore       
├── .prettierrc         
├── .prettierignore     
├── package.json
├── turbo.json
├── apps/
│   ├── web/        // frontend 작업
│   │   ├── src/
│   │   └── package.json
│   └── server/        // backend 작업
│       ├── src/
│       └── package.json
└── packages/
    └── shared/
        ├── src/
        └── package.json</code></pre><h3 id="프로젝트-생성">프로젝트 생성</h3>
<pre><code class="language-ts">yarn create turbo@latest // 새 프로젝트 생성</code></pre>
<pre><code class="language-ts">yarn add turbo -D -W</code></pre>
<blockquote>
<p>모노레포 내에서 공통적으로 사용될 설정 파일이나 UI 컴포넌트는 packages 폴더에서 관리 (eslint, prettier, ts-config 등)</p>
</blockquote>
<h3 id="apps-폴더">apps 폴더</h3>
<p>이 폴더에는 개별 프로젝트들이 위치합니다. 초기 설정으로 docs와 web이라는 두 개의 Next.js 최신 버전 프로젝트가 생성됩니다.</p>
<h3 id="packages-폴더">packages 폴더</h3>
<p>모노레포 내에서 공통적으로 사용될 설정 파일이나 UI 컴포넌트를 담는 곳입니다.
초기 상태에는 eslint-config와 ts-config가 포함되어 있으며, 공용 UI 컴포넌트도 여기에 위치합니다.</p>
<h3 id="최상위-packagejson">최상위 package.json</h3>
<p>설치를 완료하면, 다양한 스크립트 명령어가 package.json 파일에 추가됩니다. 이를 통해 최상위 폴더에서 여러 앱을 통합적으로 실행하거나 빌드할 수 있습니다.</p>
<p>Prettier, ESLint, 그리고 Turbo를 활용해 여러 스크립트를 실행할 수 있으며, 필요에 따라 추가적인 스크립트를 구성할 수 있습니다. 전역적으로 작업을 진행하고자 한다면, 이곳에 필요한 도구를 설치하고 Turbo를 통해 관리하면 됩니다.</p>
<h3 id="yarn-berry란">yarn berry란?</h3>
<p>yarn berry는 2020년 1월에 출시된 패키지 관리도구로, yarn classic에서 업그레이드된 버전입니다. yarn berry에서는 Plug’n’Play(pnp)라는 기능을 통해서 기존에 사용되던 node_modules을 사용하지 않고, .pnp.cjs라는 파일을 사용해 패키지의 의존성을 관리합니다.</p>
<p>yarn berry에서는 zero-install이라는 기능을 지원하는데, 이 기능은 프로젝트에서 사용되는 패키지를 zip으로 묶어서 캐시로 저장하고, 프로젝트를 빌드하고 배포할 때, 캐시로 저장되어 있는 패키지를 사용하기 때문에 빌드 속도를 크게 개선할 수 있습니다. 그리고 zip 파일로 저장되기 때문에 node_modules 보다 디스크의 공간을 적게 차지합니다.</p>
<pre><code class="language-ts">yarn build  //모든 애플리케이션 빌드
yarn build:web //웹 애플리케이션 빌드
yarn build:server //서버만 빌드

// 이러한 방식으로 개발환경 실행 및 배포도 구분 또는 통합하여 가능</code></pre>
<h3 id="모노레포의-장점">모노레포의 장점</h3>
<ul>
<li>코드 재사용성: 공통된 코드베이스를 여러 프로젝트에서 쉽게 재사용함으로써, 중복 코드 작성과 유지보수의 부담을 크게 줄일 수 있었습니다.</li>
<li>일관된 의존성 관리: 여러 프로젝트 간 의존성을 일관되게 관리함으로써, 업데이트와 유지보수가 용이함</li>
<li>협업의 효율성 향상: 모든 프로젝트를 하나의 리포지토리에서 관리함으로써, 팀 간 협업이 원활해지고, 개발 속도와 생산성이 크게 향상됨</li>
<li>CI/CD 파이프라인 자동화: 테스트와 린팅을 자동화하여 코드 품질을 지속적으로 유지하고, 배포 과정을 간소화함</li>
<li>캐싱 및 병렬 빌드: 프로젝트 규모가 커짐에 따라, 빌드 속도를 최적화하기 위해 캐싱과 병렬 빌드 전략을 강화할 수 있음</li>
</ul>
<p>참고자료
<a href="https://d2.naver.com/helloworld/7553804#ch3">https://d2.naver.com/helloworld/7553804#ch3</a></p>
<p><a href="https://eheh34w.medium.com/%EC%84%B1%EC%9E%A5%ED%95%98%EB%8A%94-react-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%9D%98-%ED%9A%A8%EC%9C%A8%EC%A0%81-%EA%B4%80%EB%A6%AC-turborepo%EC%99%80-vite%EB%A1%9C-%EB%AA%A8%EB%85%B8%EB%A0%88%ED%8F%AC-%EA%B5%AC%EC%84%B1%ED%95%98%EA%B8%B0-da7b5ec026d8">https://eheh34w.medium.com/%EC%84%B1%EC%9E%A5%ED%95%98%EB%8A%94-react-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%9D%98-%ED%9A%A8%EC%9C%A8%EC%A0%81-%EA%B4%80%EB%A6%AC-turborepo%EC%99%80-vite%EB%A1%9C-%EB%AA%A8%EB%85%B8%EB%A0%88%ED%8F%AC-%EA%B5%AC%EC%84%B1%ED%95%98%EA%B8%B0-da7b5ec026d8</a></p>
<p><a href="https://erwinousy.medium.com/turborepo%EC%97%90-%EB%8C%80%ED%95%9C-%EA%B0%84%EB%9E%B5%ED%95%9C-%EC%86%8C%EA%B0%9C-adf78ddb4787">https://erwinousy.medium.com/turborepo%EC%97%90-%EB%8C%80%ED%95%9C-%EA%B0%84%EB%9E%B5%ED%95%9C-%EC%86%8C%EA%B0%9C-adf78ddb4787</a>
<a href="https://engineering.linecorp.com/ko/blog/monorepo-with-turborepo#3">https://engineering.linecorp.com/ko/blog/monorepo-with-turborepo#3</a></p>
<p><a href="https://geekk89.medium.com/turborepo-%EC%B0%8D%EB%A8%B9-%ED%95%B4%EB%B3%B4%EA%B8%B0-e9e160864c23">https://geekk89.medium.com/turborepo-%EC%B0%8D%EB%A8%B9-%ED%95%B4%EB%B3%B4%EA%B8%B0-e9e160864c23</a></p>