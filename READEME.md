## Viewport

### 설명

- 뷰포트는 현재 보고 있는 컴퓨터 그래픽의 영역을 나타낸다. **즉 뷰포트는 웹 페이지에서 브라우저가 화면상에 실제로 표시되는 영역** 이므로 **사용자가 볼 수 있는 시각적인 영역** 이다.
- 같은 페이지라고 하더라도 모바일과 태블릿은 화면 크기가 다르다. 화면 크기가 다르다면 사용자가 볼 수 있는 범위가 달라지게 된다.

#### Layout Viewport 와 Visutal Viewport
* 모바일 브라우저에는 Layout Viewport 와 Visutal Viewport 2가지 뷰포트가 존재하게 된다. Layout viewport 의 경우 고정된 화면이므로 사용자의 action 에 영향을 받지 않는다. 반대로 visual viewport 의 경우는 사용자의 action, 즉 손가락으로 화면을 확대하는 등의 경우에 영향을 받아서 크기가 변하개 된다.

![image](https://user-images.githubusercontent.com/41986911/116081793-a582f500-a6d5-11eb-813a-c8a912081396.png)

### 예제

1. Viewport 설정하기

- HTML5 에서는 meta 태그를 이용해서 뷰포트를 컨트롤 할 수 있도록 제공하고 있다. 아래와 같은 코드를 선언함으로서 뷰포트를 사용하겠다는 것을 명시한다.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

- 뷰포트를 설정하지 않은 경우 모바일 환경과는 달리 데스크탑 환경에서는 뷰포트를 설정한 경우와 그렇지 않은 경우 같은 페이지를 볼 수 있다. 하지만 모바일 환경에서는 아래와 같은 결과의 차이를 보여준다.

![image](https://user-images.githubusercontent.com/41986911/116075833-67ce9e00-a6ce-11eb-8349-3897624d9531.png)

- 뷰포트를 설정하지 않은 경우에는 모바일에서 볼 수 있는지 의아할 정도의 크기로 확대를 해서야 겨우 볼 수 있었다. 뷰포트를 설정한 경우 데스크탑 기기에서 볼 때 만큼 깔끔하게 보이지는 않았지만, 사용자의 화면에 맞춰 글자나 이미지등을 확대해서 보여주었다.

2. 네이버의 Viewport

- 가장 친숙한 네이버 사이트에서는 뷰포트를 어떻게 설정해줬을까 궁금해서 찾아보니 minimum-scale 과 maximum-scale 은 전부 1.0으로 지정하고, user-scalable 을 no 로 지정했다.

```html
<meta
  name="viewport"
  content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no"
/>
```

- 이 코드를 통해 네이버는 최소 배율값과 최대 배율값을 같게 만들어주고, 사용자의 zoom-in, zoom-out 을 할 수 없도록 막아두었기 때문에 항상 고정된 UI 를 보여주려고 한 것 같다.

- 접근성 검사를 돌려보니 이 경우에는 경고를 받을 수 있다. validator.w3.org 에서는 아래와 같은 경고를 날린다.

![image](https://user-images.githubusercontent.com/41986911/116075628-2211d580-a6ce-11eb-96ef-841d67acd66a.png)

- 사용자의 문서 리사이징을 막는 것을 피해달라는 경고를 표출한다. 아마 이 부분은 웹 접근성과 관련 있는 경고처럼 보인다.


#### 속성

1. initial-scale=1

- 원본의 크기를 출력하는 것을 의미한다. 즉, initial-scale 이 1 이라는 것은 기기의 픽셀과의 1:1 관계를 의미하고, 만약 2로 바꾼다면 2배 더 커진 텍스트를 확인이 가능하다. (0~10 사이의 값을 사용할 수 있다.)

2. width=device-width

- 페이지의 너비를 장치의 화면 너비를 따르도록 설정한다. 페이지의 너비를 기기의 스크린 너비로 설정해주기 때문에 렌더링 영역을 기기의 뷰포트와 같게 만들어주는 역할을 한다.

3. minumum-scale

- 뷰포트의 최소 배율값을 설정할 수 있다. (0~10 사이의 값을 사용할 수 있다.)

4. maximum-scale

- 뷰포트의 최대 배율값을 설정할 수 있다. (0~10 사이의 값을 사용할 수 있다.)

5. user-scalable

- 사용자의 브라우저를 확대/축소 여부를 설정한다. yes 와 no 중 하나를 선택해서 적용이 가능하고 뷰포트에서 가장 접근성과 연관되어 있는 값이다. 확대와 축소는 사용성에 큰 영향을 미칩니다. 만약 뷰포트에서 지정한 크기를 볼 수 없는 문제가 발생한 경우 확대를 통해 사용성을 높일 수 있다.
- w3.org 에서 접근성 관련 규정으로 지정되어 있다
  - 1.4.4 텍스트 크기 조정(Level AA), 1.4.10 리플 로우(Level AA)
    - 콘텐츠의 경우 정보나 기능의 손실이 없도록 양방향으로 스크롤 되지 않도록 제공해야 한다.
    - 만약 각 줄을 읽을 때 좌우로 스크롤을 해야 한다면 혼란스럽고, 읽고 있는 내용을 이해하기 어렵게 만들 수 있다.
    - Adobe Reader 의 경우 Reflow 기능을 켜면 스크롤 바가 한 방향에만 생겨 콘텐츠를 읽기 편해진다.
    - ![image](https://user-images.githubusercontent.com/41986911/116077154-1e7f4e00-a6d0-11eb-94ae-fc61a3456024.png)

6. shrink-to-fit
- 애플의 사파리 11 버전에서 뷰토프의 크기가 보여줘야 할 내용보다 작으면 보여줘야 할 내용을 줄여서 보여준다. 다른 브라우저에서는 사용되지 않는 값이라고 한다. 크로스 브라우징이 정말 어려운 것이구나를 한 번 더 느끼게 된 속성이다.

### 호환성


### 출처
[네이버 nuli](https://nuli.navercorp.com/community/article/1132729)
[W3school](https://www.w3schools.com/css/css_rwd_viewport.asp)
[MDN Viewport](https://developer.mozilla.org/en-US/docs/Web/CSS/Viewport_concepts)
[2019 널리세미나 WCAG 2.1](https://www.slideshare.net/NULINTS/2019-wcag-21-reflow-153332260)
