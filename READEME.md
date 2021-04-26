## 미디어 쿼리(Media Query)
미디어 쿼리는 다양한 기기 특성과 어떤 특성이나 수치에 따라 웹 사이트, 혹은 앱을 조정할 수 있는 요소이다.  
  
미디어 쿼리를 사용하여 반응형 웹을 만드는 방법
### 1. CSS에서의 미디어 쿼리  
CSS 파일 안에서 @media나 @import같은 @규칙을 사용하여 스타일 시트의 일부를 조건부로 적용하는 방법

@import는 CSS 엔진에게 외부 스타일 시트를 포함하도록 알린다.
@media는 장치가 미디어 쿼리를 사용하여 정의된 조건의 기준을 만족하면 해당 콘텐츠를 적용하는 조건부 그룹 규칙이다.  

복잡한 쿼리 조합하기
> @media only | not 미디어 유형 and |, (조건문) {적용할 css}

### 예제
ex1. 아래와 같이 @media에 max-width와 min-width 미디어 기능을 사용하여 화면의 너비에 따라 배경색이 변경되도록 했다.
```css
@media (min-width: 801px){ 801px ~ : coral}
```
  
논리 연산자
not, and, only와 같은 논리 연산자를 이용해 복잡한 쿼리를 조합할 수 있다.  
+ and 연산자  
    다수의 미디어 특성을 조합하여 하나의 미디어 쿼리를 만들 때 사용한다. 쿼리가 참이려면 모든 구성 특성이 참을 반환해야 한다. 미디어 유형을 같이 사용할 때도 쓰인다.
+ not 연산자
    미디어 쿼리를 부정하여, 쿼리가 거짓일 때만 참을 반환한다.
    쉽표로 구분한 쿼리 목록 중 하나에서 사용한 경우, 전체 쿼리가 아닌 해당하는 하나의 쿼리에만 적용된다. not 연산자를 사용할 경우 반드시 미디어 유형도 지정해야 한다.
+ only 연산자
    전체 쿼리가 일치할 때만 스타일을 적용할 때 사용하며, 오래된 브라우저가 스타일을 잘못 적용하지 못하도록 방지할 때 유용하다.
+ ,(쉼표)
    다수의 미디어 쿼리를 하나의 규칙으로 조합할 때 사용한다. 쉼표 목록 내의 쿼리 각각은 나머지와 별개로 취급하므로, 단 하나의 쿼리만 참을 반환해도 규칙 전체가 참이 된다. 즉, 쉼표는 논리 연산자 or 처럼 동작한다.
  
미디어 유형
주어진 장치의 일반적인 분류를 설명한다.
다른 유형이 특정되지 않았을 땐 all이 기본값으로 적용된다.  
하지만 사용자가 not이나 only 연산자를 사용하면, 사용자는 반드시 미디어 유형을 특정해야한다.

+ all
모든 장치에 적합할 때 사용한다.  

+ screen
일반적으로 화면을 대상으로 할 때 사용한다.
> @media screen {...}

+ print
프린터 장치를 대상으로 할 때 사용한다.
> @media print {...}

+ speech
음성 합성장치를 대상으로 할 때 사용한다.

+ print, screen
다수의 장치를 특정할 수도 있다.
> @media print, screen {...}

  
### 2. HTML에서의 미디어 쿼리  
 HTML의 &lt;style&gt; 요소, &lt;link&gt; 요소, &lt;source&gt; 요소 등의 HTML 요소의 media 속성에 값을 설정하는 방법
  
+ style 요소 사용  
> &lt;style type="text/css" media=＂미디어유형 and (조건문)"&gt;
  
> 이때, &lt;link&gt;의 미디어 쿼리가 거짓을 반환하더라도 스타일 시트는 다운로드 된다. 하지만, 그 안의 내용은 미디어 쿼리가 참이 되어야 적용된다.

### 예제
ex2. 아래와 같이 style 태그를 이용하여 max-width와 min-width 미디어 기능을 사용하여 화면의 너비에 따라 배경색이 변경되도록 했다.
```css
<style type="text/css" media="all and (max-width: 800px)">
    body {
        backgr ound-color: pink;
    }
</style>
```

> &lt;link rel="stylesheet" media="미디어유형 and (조건문)" href="조건이 참일 때 적용할 css링크주소"/&gt;

### 예제
ex3. 아래와 같이 link 태그를 이용하여 max-width와 min-width 미디어 기능을 사용하여 화면의 너비에 따라 배경색이 변경되도록 했다.
```css
<link rel="stylesheet" media="screen and (max-width: 800px)" href="./css/media_query_ex3_600px_800px.css"/>
```

### 3. JavaScript에서의 미디어 쿼리
Window.matchMedia(), MediaQueryList.addListener() 메서드를 사용하여 미디어 상태를 판별하여 

### 예제
이는 html/css가 끝나고 javascript를 배운 후에, 예제 실습을 해보도록 하겠다.









### 호환성