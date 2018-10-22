###### Chapter6 컴포넌트 기초

##### 컴포넌트 조합
Vue.js는 컴포넌트들을 조합해 하나의 애플리케이션을 만든다.
조합된 컴포넌트들은 부모-자식 관계인 트리 구조를 형성하며
부모와 자식 컴포넌트 간의 정보 전달은 props와 event를 사용하여 정보를 전달한다.
<img src="./img/component_struct.png" width="841px" height="343px"></img>


##### 컴포넌트의 작성
~~~javascript
Vue.component(tagname, options)
~~~
* __tagname__: 컴포넌트를 사용할 태그명이다.
* __options__: 컴포넌트에서 렌더링할 template 등을 지정한다.

tagname은 대소문자를 구분하지 않기 때문에 파스칼(pascal)/카멜(camel) 표기법이 아닌 케밥(kebob) 표기법을 사용한다.
options는 Vue 인스턴스의 옵션과 같이 data, methods, computed, watch 옵션을 사용할 수 있다.





##### DOM 템플릿 구문 작성 시 주의 사항

##### 컴포넌트에서의 data 옵션

##### props와 event

##### 이벤트 버스 객체를 이용한 통신
