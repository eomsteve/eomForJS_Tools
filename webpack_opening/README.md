# Webpack?

## 웹팩이란

웹팩이란 `모듈 번들러`이다. 

**모듈**이란 구현 세부사항을 캡슐화 하고 공개 API를 노출하여 다른 코드에서 쉽게 로드하고 사용할 수 있도록 재사용 가능한 코드조각이다.

`웹팩에서 모듈은 웹 애플리케이션을 구성하는 모든 자원`

### 모듈 사용의 장점

* 자주 사용되는 코드를 별도의 파일로 만들어서 필요할 때마다 재활용할 수 있다.
* 코드를 개선하면 이를 사용하고 있는 모든 애플리케이션의 동작이 개선된다.
* 코드 수정 시에 필요한 로직을 빠르게 찾을 수 있다.
* 필요한 로직만을 로드해서 메모리의 낭비를 줄일 수 있다.
* 한번 다운로드된 모듈은 웹브라우저에 의해서 저장되기 때문에 동일한 로직을 로드 할 때 시간과 네트워크 트래픽을 절약 할 수 있다. (브라우저에서만 해당)


**번들**이란 소프트웨어 및 일부 하드웨어와 함께 작동하는데 필요한 모든것을 포함하는 패키지 이다.

그래서 **모듈번들러**란 우리가 만들려는 프로젝트에 필요한 모든 코드조각(모듈)들을 포함시켜주는 도구이다.
>웹 애플리케이션을 구성하는 자원(HTML, CSS, JS, Img등)을 모두 각각의 모듈로 본다.
>>  JavaScript 모듈을 브라우저에서 실행할 수 있는 단일 JavaScript 파일로 번들링하는데 사용되는 프론트엔드 개발 도구


# 웹팩 등장 배경

1. 파일단위 자바스크립트 모듈단위 관리의 필요성
2. 웹 개발 작업 자동화 도구(Web Task Manager)
3. 웹 애플리케이션의 빠른 로딩 속도와 높은 성능

## 파일단위 자바스크립트 모듈단위 관리의 필요성

과거엔 웹페이지와 웹 서비스의 규모가 크지않아 이를 구성하는 HTML파일과 JS파일의 크기도 상대적으로 작았고, 해당 서비스를 유지하는데 큰 무리가 없었다. 
> 최초의 JavaScript는 아주 간단한 모듈 시스템만을 제공했다. 바로 HTML에서 JavaScript 원본 소스를 제공하고, 브라우저에서 이것을 순서대로 로드하는 방식

대규모 웹 서비스의 등장으로 하나의 웹 서비스에서 여러개의 자바스크립트 파일을 다루게 되며 문제가 발생했다.

모듈간의 스코프가 구분이 되지않아 다른 파일을 오염시키는 경우가 발생하게 되고, 다른 모듈과 변수 이름이 겹치지 않도록 모듈 로드 순서를 지정하는데 많은 시간을 할애하게 되었다.

즉, 스코프가 구분되는 모듈이 필요해졌고, JavaScript모듈을 브라우저에서 실행할수 있는 단일 JavaSrcipt 파일로 번들링하기 위해 모듈번들러가 처음 만들어졌다.


### 2. 파일 전송 문제

사용자가 브라우저에서 URI를 입력하면 입력한 URI에 해당하는 파일을 서버로 부터 가져온다. 여기서 웹 애플리케이션를 구성하는 파일의 양이 많다면, 사용자의 요청에 응답하는 시간이 길어지게 된다.

만약, 파일들의 크기가 엄청 커서 1개의 파일을 요청하고 응답하는데 1초가 걸린다고 한다면 100개의 파일을 응답하는 데 100초, 1000개의 파일을 응답하는 데 1000초의 시간이 걸리는 끔찍한 사용자 경험을 선사하게된다. 사용자뿐만 아니라 서비스를 제공하는 입장에서도 엄청난 양의 파일을 주고 받으면서 생기는 비용적인 문제가 발생할 것이다.

하나의 파일안에 모든 스크립트를 작성한다면 이러한 문제를 해결 할 수 있겠지만 유지보수 측면에서 봤을 때에는 상당히 좋지 못한 방법이다.

위의 문제들을 해결하기 위해 여러개의 파일을 하나의 파일로 묶어주는 번들러(Bundler)가 등장했다.


## 웹 개발 작업 자동화 도구(Web Task Manager)

개발 과정에서 코드를 작성하고, 컨벤션을 유지하기 위해 린트를 사용하며, Sass나 TypeScript처럼 전처리가 필요한 언어를 컴파일하고, 소스 코드를 축소(minify)하고 하나의 파일로 묶는(bundle) 일련의 과정들이 필수적으로 동반된다. 이러한 과정들의 `반복`은 이러한 특정 작업들을 자동화 할 수 있는 도구의 필요성 으로 이어졌고, 그 결과물이 바로 태스크 러너(task runner)이다. 즉, 태스크 러너는 태스크 러너는 프로덕트 개발 과정에서 필요한 일련의 과정들(린팅, 빌딩, 테스팅 등)을 자동화하기 위한 도구이다.

* HTML, CSS, JS 압축
* 이미지 압축
* CSS 전처리기 변환

# WEBPACK

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcNBE4q%2Fbtq4K9syJFE%2FKboaLr30F7STXxdVqsLUI0%2Fimg.png)

웹팩등장 배경을 이해하고 나면 위 그림이 의미하는것을 한눈에 알수있다.

**웹팩**은 프로젝트에 필요한 모든 의존성 파일들을 하나의 번들파일로 만들어주어 배포하기 쉽게 빌드해 주는 도구이다.

 웹팩은, 오래된 만큼 생태계가 풍부하고 안전성이 뛰어난 번들러이다.

웹팩은 웹 애플리케이션에서 사용하는 CSS나 이미지 같은 에셋들을 JavaScript 코드로 변환하고, 이를 분석해서 번들하는 방식을 사용한다. 그렇기 때문에 웹팩의 구성은 다른 번들러에 비해 설정할 게 많고, 복잡하다.

그리고 ES6 모듈 형태로 빌드 결과물을 출력할 수 없다는 단점이 있다.

