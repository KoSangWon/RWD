유동형 이미지
- 이미지의 크기가 브라우저의 창 크기에 따라 자동으로 줄어들고 늘어나는 것을 의미합니다.
- 일반적으로 브라우저상의 이미지는 고정된 크기를 가지고 있지만, 반응형 웹 디자인에서는 이미지가 브라우저의 창 크기에 맞게 적절한 형태로 변경될 수 있도록, 창의 가로너비에 유동적으로 변하는 단위를 사용합니다.
![image](https://user-images.githubusercontent.com/49035066/116072886-a3ffff80-a6ca-11eb-8e70-0a74fdb739d5.png)

## 구현 방법
### 1.&lt;picture&gt; 태그
- <picture> 요소는 0개 이상의 <source> 요소와 하나의 <img> 요소로 구성되며, 브라우저는 <source> 요소 중에서 해당 뷰포트와 가장 잘 어울리는 <source> 요소를 다음과 같은 방법을 사용하여 선택합니다.
- 브라우저는 <source> 요소들의 속성값을 각각 확인해 나가며 조건을 만족하는 첫 번째 <source> 요소를 사용하고, 나머지 <source> 요소들은 무시합니다. 이 때 <img> 요소는 <picture> 요소의 자식 요소 중에서 가장 마지막에 위치해야 합니다. 


```HTML
<picture>
    <source media="(min-width: 700px)" srcset="/examples/images/people_960.jpg">  <!-- 뷰포트 너비가 700px이상인 경우  --> 
    <source media="(min-width: 400px)" srcset="/examples/images/people_575.jpg">  <!-- 뷰포트 너비가 400px이상인 경우 -->
    <img src="/examples/images/people_200.jpg" alt="People">                      <!-- 웹 브라우저에서 <picture>태그를 지원하지 않는 경우 -->
</picture>
```
![image](https://user-images.githubusercontent.com/49035066/116074736-1a056600-a6cd-11eb-9f0e-aee925fa9ed8.png)


### 2.&lt;img&gt;태그의 속성(sizes, srcset)
#### srcset
     1. 사용자 에이전트가 사용할 수 있는 이미지 소스의 후보. 쉼표로 구분하는 한 개 이상의 문자열 목록입니다.
     2. srcset = "이미지URL 너비서술자(w) 밀도서술자(x)" 구조로 입력합니다.
     3. 밀도 서술자를 포함하지 않은 경우 기본값인 1x로 간주합니다.
#### sizes
    1. 속성은 쉼표(,)로 구분된 미디어조건(선택적)과 그에 따라 최적화되어 출력될 이미지 크기를 지정합니다.
    2. sizes = "미디어조건 소스크기값" 구조로 입력합니다.
    3. 마지막 sizes 항목에서는 미디어조건을 생략해야 합니다.
    4. 소스 크기는 의도한 이미지 표시 크기를 지정합니다. 사용자 에이전트는 현재 소스 크기를 사용해, 너비(w) 서술자를 사용한 srcset 특성의 소스 중 하나를 선택합니다.


#### 예시
```HTML
<img
  srcset="images/heropy_small.png 400w,    <!-- 뷰포트 너비가 400px 이하일 때 heropy_small.png(400px)가 사용됩니다. -->
          images/heropy_medium.png 700w,   <!-- 뷰포트 너비가 401~700px 일 때 heropy_medium.png(700px)가 사용됩니다. -->
          images/heropy_large.png 1000w"   <!-- 뷰포트 너비가 701~999px 일 때 heropy_large.png(1000px)가 사용됩니다. -->
  sizes="(min-width: 1000px) 700px"     <!-- 뷰포트 너비가 1000px 이상일 때 heropy_medium.png(700px)가 사용됩니다. -->
  src="images/heropy.png"               <!-- 웹 브라우저에서 srcset, sizes 속성을 지원하지 않는 경우 -->
  alt="HEROPY" />
```

![image](https://user-images.githubusercontent.com/49035066/116075984-9c425a00-a6ce-11eb-9bd1-41f9c3ef36f9.png)


## 미디어 쿼리(Media Query)
미디어 쿼리는 다양한 기기 특성과 어떤 특성이나 수치에 따라 웹 사이트, 혹은 앱을 조정할 수 있는 요소이다. 이를 이용해 반응형 웹사이트 혹은 앱을 만들 수 있다.
  
### 1. CSS에서의 미디어 쿼리  
+ CSS 파일 안에서 @media나 @import같은 @규칙을 사용하여 스타일 시트의 일부를 조건부로 적용하는 방법

+ @import는 CSS 엔진에게 외부 스타일 시트를 포함하도록 알린다.
+ @media는 장치가 미디어 쿼리를 사용하여 정의된 조건의 기준을 만족하면 해당 콘텐츠를 적용하는 조건부 그룹 규칙이다.  

+ 복잡한 쿼리 조합하기
> @media only | not 미디어 유형 and |, (조건문) {적용할 css}

### 예제 ex1
아래와 같이 @media에 max-width와 min-width 미디어 기능을 사용하여 화면의 너비에 따라 배경색이 변경되도록 했다.
```css
@media (min-width: 801px){ 801px ~ : coral}
```
[Media Query 예제1](https://hyunjungc-dev.github.io/RWD_practice/media_query_ex1.html)

+ 논리 연산자
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
  
+ 미디어 유형
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

### 예제 ex2
아래와 같이 style 태그를 이용하여 max-width와 min-width 미디어 기능을 사용하여 화면의 너비에 따라 배경색이 변경되도록 했다.
```css
<style type="text/css" media="all and (max-width: 800px)">
    body {
        backgr ound-color: pink;
    }
</style>
```
[Media Query 예제2](https://hyunjungc-dev.github.io/RWD_practice/media_query_ex2.html)


+ link 요소 사용
> &lt;link rel="stylesheet" media="미디어유형 and (조건문)" href="조건이 참일 때 적용할 css링크주소"/&gt;

### 예제 ex3
아래와 같이 link 태그를 이용하여 max-width와 min-width 미디어 기능을 사용하여 화면의 너비에 따라 배경색이 변경되도록 했다.
```css
<link rel="stylesheet" media="screen and (max-width: 800px)" href="./css/media_query_ex3_600px_800px.css"/>
```
[Media Query 예제3](https://hyunjungc-dev.github.io/RWD_practice/media_query_ex3.html)

### 3. JavaScript에서의 미디어 쿼리
Window.matchMedia(), MediaQueryList.addListener() 메서드를 사용하여 미디어 상태를 판별하여 

### 예제 ex4
이는 html/css가 끝나고 javascript를 배운 후에, 예제 실습을 해보도록 하겠다.

### 예제 ex1 ~ ex3
600px 미만에선 background color가 cornflowerblue색이 적용되고
![600px미만](https://github.com/HyunJungC-Dev/RWD/blob/main/04_team/assets/MQex3.PNG)
601~800px에선 background color가 pink색이 적용되고
![601~800px](https://github.com/HyunJungC-Dev/RWD/blob/main/04_team/assets/MQex2.PNG)
801px 이상에선 background color가 coral색이 적용된다.
![801px 이상](https://github.com/HyunJungC-Dev/RWD/blob/main/04_team/assets/MQex1.PNG)


## 유동형 그리드(Fluid Grid)
### 설명
- Grid는 웹페이지를 위한 이차원 레이아웃 시스템이다. 이 기능을 통해 콘텐츠를 행과 열에 배치할 수 있으며 복잡한 레이아웃을 직접 직관적으로 구축 가능하다. 
- Fluid Grid란 웹사이트를 제작할 때 화면의 크기에 관계없이 자유롭게 늘어나거나 줄어들 수 있도록 픽셀(px) 대신 퍼센트(%)로 제작하는 기술이다. Grid의 너비를 Flexible Image와 마찬가지로 창의 너비에 대응되는 가변 너비로 설정한다.

#### Fluid Grid의 중요성
- 적응 형 그리드에서는 픽셀 기반으로 크기를 지정한다. 따라서 특정 장치 viewport에서 너비와 높이를 수동으로 조정해야한다. 유동 격자는 상위 컨테이너의 크기 내에서 자연스럽게 흐르기 때문에 다양한 화면 크기와 장치에 대한 대응이 가능하다.
- 모바일 크기가 점점 작아지고 있고 반면 데스크톱은 해상도가 높아질수록 점점 더 넓어지고 있다. 유동형의 장점은 최대 너비를 조정할 수 있으며 백분율 기반 계산으로 인해 더 큰 화면에서 계속 작동할 수 있다는 것이다.


#### Fluid Grid 실제 적용 사례
- [palantir.net](https://www.palantir.net/services)
- 아래 예시에서 웹페이지의 너비가 작아질수록 유동적으로 변하는 모습을 볼 수 있다. 
<img src="./assets/fluid-grid-1.gif" width="800">

### 예제
#### Fluid Grid 계산
- 디자인한 Grid의 간격을 측정한 뒤, 전체 페이지에서 하나의 Grid가 차지하는 공간이 몇 `%`인지를 계산하여 가변단위인 `%`로 값을 설정해 주면 Grid가 창 너비에 따라 가변적으로 변하여 동작할 수 있다.

    1. 가변 너비 
        - (가변 크기로 만들 박스의 가로 너비 / 가변 크기로 만들 박스를 감싸고 있는 박스의 가로 너비) * 100 = 가변 크기의 %값
        
        - 위 예시처럼 퍼센트를 사용해 그리드의 크기를 정해주면 사용자가 사용하는 브라우저의 크기에 맞춰 개발이 가능하다.
        - 브라우저의 크기가 변하거나 사용하는 디바이스의 크기에 맞춰 자동으로 변하는 컨텐츠를 기대할 수 있다.

    2. 가변 마진
        - 웹 사이트의 요소에 마진과 패딩을 설정할 때는 모든 박스들을 감싸고 있는 요소들의 너비값을 고려하여 요소의 마진값과 패딩값을 지정해야 한다. 
        - 만약 너비값을 고려하지 않고 마진값과 패딩값을 설정하면 박스들이 밀려 아래로 떨어지는 등 의도했던 대로 레이아웃이 나오지 않을 수 있다.
        - 반응형 웹사이트에서는 모든 요소는 가변적이어야 한다.
        - (가변 마진을 적용할 마진값 / 적용할 박스를 감싸고 있는 박스의 가로 너비) * 100 = 가변 마진 % 값

    3. 가변 패딩
        - (가변 패딩을 적용할 패딩값 / 적용할 박스를 감싸고 있는 박스의 가로 너비) * 100 = 가변 패딩 % 값

- 유동형 그리드 HTML, CSS 예시
    - HTML
        ```html
        <div id="wrap">
            <div class="container">
            <div id="first"></div>
            <div id="second"></div>
            </div>
        </div>
        ```
    - CSS
        ```css
        #wrap {
            width: 80%;
            height: 500px;
            ...
        }

        .container {
            width: 80%;
            height: 450px;
            ...
        }

        #first {
            width: 33.33%;
            background-color: aqua;
        }

        #second {
            width: 66.67%;
            background-color: greenyellow;
        }

        ...
        ```

- 결과
<img src="./assets/fluid-grid-2.gif" width="800">
    - 각 컨테이너의 너비가 유동적으로 화면의 크기에 따라 유동적으로 달라짐을 확인할 수 있다.
