# Chapter6 컴포넌트 기초


### 컴포넌트의 조합
Vue.js는 컴포넌트들을 조합해 하나의 애플리케이션을 만든다.<br>
조합된 컴포넌트들은 부모-자식 관계인 트리 구조를 형성하며
부모와 자식 컴포넌트 간의 정보 전달은 props와 event를 사용하여 정보를 전달한다.
<img src="../img/component_struct.png" width="900px" height="368px"></img>


### 컴포넌트의 작성
~~~javascript
Vue.component(tagname, options)
~~~
* __tagname__: 컴포넌트를 사용할 태그명이다.
* __options__: 컴포넌트에서 렌더링할 template 등을 지정한다.

tagname은 대소문자를 구분하지 않기 때문에 파스칼(pascal)/카멜(camel) 표기법이 아닌 케밥(kebob) 표기법을 사용한다.<br>
options는 Vue 인스턴스의 옵션과 같이 data, methods, computed, watch 옵션을 사용할 수 있다.

> example01: 인라인(템플릿 옵션에 템플릿 문자열을 사용) 템플릿을 사용한 예제
>> ~~~javascript
>> <div id="app">
>>     <hello-component></hello-component>
>>     <hello-component></hello-component>
>>     <hello-component></hello-component>
>> </div>
>>
>> <script type="text/javascript">
>>     Vue.component('hello-component', {
>>       template: '<div>hello world</div>',
>>     });
>>
>>     var v = new Vue({
>>       el: '#app',
>>     });
>> </script>
>> ~~~

> example02: 템플릿 문자열을 포함하고 있는 ```<template>``` 태그를 사용한 예제
>> ~~~javascript
>> <div id="app">
>>     <hello-component></hello-component>
>>     <hello-component></hello-component>
>>     <hello-component></hello-component>
>> </div>
>>
>> <template id="helloTemplate">
>>     <div>hello world!!!</div>
>> </template>
>> <script type="text/javascript">
>>     Vue.component('hello-component', {
>>         template: '#helloTemplate',
>>     });
>>
>>     var v = new Vue({
>>       el: '#app',
>>     });
>> </script>
>> ~~~

> example03: 템플릿 문자열을 포함하고 있는 ```<script type="text/x-template">``` 태그를 사용한 예제
>> ~~~javascript
>> <div id="app">
>>     <hello-component></hello-component>
>>     <hello-component></hello-component>
>>     <hello-component></hello-component>
>> </div>
>>
>> <script type="text/x-template" id="helloTemplate">
>>     <div>hello world!!!</div>
>> </script>
>> <script type="text/javascript">
>>     Vue.component('hello-component', {
>>         template: '#helloTemplate',
>>     });
>>
>>     var v = new Vue({
>>       el: '#app',
>>     });
>> </script>
>> ~~~


### DOM 템플릿 구문 작성 시 주의 사항
1. 자식노드를 포함하는 요소에 대한 Vue 컴포넌트의 오류
~~~html
<div id="app">
    <select>
        <option-component></option-component>
        <option-component></option-component>
    </select>
</div>

<script type="text/javascript">
    Vue.component('option-component', {
      template: '<option>hello</option>'
    });

    var v = new Vue({
      el: '#app',
    });
</script>
~~~
 - HTML 요소들은 자식 요소를 포함 시킬 수 있으며 어떤 요소들은 자식 요소가 정해져 있는 경우가 있다.
 - 위의 예제를 살펴보면 ```<select>``` 요소는 ```<option>``` 요소를 필수 자식 노드로 가지게 되는데
코드 상에는 ```<option-component>``` 컴포넌트가 자식 노드로 배치되어 있다.
이 경우 Vue 컴포넌트를 렌더링하기 전 구문 분석을 수행하게 되는데 구문 분석 단계에서 DOM 요소가 올바르지 않다고 판단하고
정상적인 렌더링을 수행하지 못하는 문제가 발생하게 된다.
 - 이 문제를 해결하기 위해서는 is 속성을 사용하면 된다.
~~~html
<select>
    <option is="option-component"></option>
    <option is="option-component"></option>
</select>
~~~
 - .vue 확장자를 사용하는 단일 파일 컴포넌트(Single File Component)를 작성하는 경우에는 사용하지 않아도 된다.
 - ```<template>``` 태그를 사용할 때는 is 속성을 사용해야 한다.

2. 템플릿 문자열 안에는 Root Element는 반듯이 하나여야 한다. 여러개의 Root Element가 존재할 경우 오류가 발생함으로
<div>로 한 번 더 감싸주어 오류를 해결할 수 있다.
> 오류가 발생하는 코드
~~~html
<template id="helloTemplate">
    <div>hello</div>
    <div>hello</div>
</template>
~~~

> 정상적으로 동작하는 코드
~~~html
<template id="helloTemplate">
    <div>
        <div>hello</div>
        <div>hello</div>
    </div>
</template>
~~~


### 컴포넌트에서의 data 옵션

### props와 event

### 이벤트 버스 객체를 이용한 통신
