# React-express_inflearn
(1) 인프런 - "React &amp; Express 를 이용한 웹 어플리케이션 개발하기"  - 버전 문제로 중단 (2018 강의)<br/>
(2) 노마드 코더 - "ReactJS로 영화 웹 서비스 만들기" https://nomadcoders.co/react-fundamentals/lectures/1540

### Setting : Git, NPM/Node, MongoDB, 

ReactJS 

장점
- 프레임워크가 아닌 라이브러리 
- 가상돔을 사용 
- component 개념 
- <b>뛰어난</b> garbage collection / 메모리 관리 / 성능
- 서버 & 클라이언트 렌더링
- UI 재사용화
- 다른 프레임워크나 라이브러리와 혼용가능


단점
- VIEW ONLY (데이터 모델링, 라우팅, AJAX 등등 X) -> 다른 라이브러리를 추가하여 구현
- IE8 이하 지원 X
<br>
<b>개발환경 설정</b>

- babel (javascript preprocessor) - ES6를 ES5 이전 버전으로 변환
- react 컴파일 담당
- react-dom - 렌더링 담당
- react <b>JSX</b> - xml 같은 문법을 native javascript로 변환시켜줌


비고
- '…' 은 자바스크립트의 전개연산자 입니다. 기존의 객체안에 있는 내용을 해당 위치에다가 풀어준다는 의미죠. 그 다음에, 우리가 설정하고 싶은 값을 또 넣어주면 해당 값을 덮어쓰게 됩니다.
- es6의 arrow function 문법
- components - html을 반환하는 함수 
- jsx = javascript + html
- react는 하나의 component만 렌더링 할 수 있다. (버전별 확인 필요) / + styling

--------
### JSX
>1.Nested Element
- 컴포넌트에서 여러 Element를 렌더링 할 때 꼭 container element 안에 포함시켜야 함

``` react.js
    render() { 
      return ( 
        <div>
          <h1>Hi<hi>
        </div>
      ) 
    }
```



>2.JavaScript Expression
- JSX안에서 JavaScript를 표현하는 방법 - { } 로 wrapping
- let : 블록 유효 범위를 갖는 지역 변수 선언 구문, 임의로 값을 초기화 가능, 한번 선언후 재선언 불가
``` react.js
    render() {
        let text = "Hello React!";
        return (
            <div>{text}</div>
        );
    }
```
- if else 문은 JSX에서 사용불가 - 이에 대한 대안은 tenary expression 
> condition ? true : false
``` react.js
    render() {
       return (
        <p> {1==1 ? 'True' : 'False'} </p>
       );
    }
```
>3.Inline Style
- JSX안에서 Style 설정시 string 형식을 사용하지 않고 key가 CamelCase인 객체 사용
``` react.js
    render() { 
      let style = {
        color:'aqua',
        backgroundColor:'black'
      };
      
      return ( 
        <div style={styls}>React CodeLab</div>
      ); 
    }
 ```
 
 
 - JSX안에서 class 설정 시 class = 가 아닌 className = 을 사용
``` react.js
    render() { 
      return ( 
        <div className="box">React CodeLab</div>
      ); 
    }
```


>4.Comments
- JSX안에서 주석 작성시 { /* ... */ } 
- Nested Element 부분에 설명했던 것과 같이 container element 안에 주석이 작성되어야 함
``` react.js
    render() { 
      return ( 
        <div>
            { /*This is How You Comment*/}
            { /*Multi-line
                Testing*/}
            React CodeLab
        </div>
      ); 
    }
```



--------
### props
- 컴포넌트 내부의 Immutable Data
- JSX 내부에 { this.props.propsName }
- 컴포넌트를 사용할 때 , <> 괄호 안에 propsName = "value"
- <i>this.props.children</i> 은 기본적으로 갖고 있는 props로서, <Cpnt> 여기에 있는 값이 들어간다. </Cpnt>
- 프로퍼티의 속성을 es6 문법을 사용하여 단순하게 표기할 수 도 있다.
``` react.js
function Food({fav}) {
  return <h1>I like {fav}</h1>;
}


function Food(props.fav) {
  return <h1>I like {props.fav}</h1>;
}
``` 


``` react.js
class Codelab extends React.Component {
  render(){
     return (
      <div> /*~~*/
         <h1>Hello {this.props.name}</h1>
         <div>{this.props.children}</div>
      </div>
     );
  }
}

class App extends React.Component {
  render() {
    return (
      <Codelab name={this.props.name}>{this.props.children} </Codelab>  
    );
  }
}

ReactDOM.render(<App name="velopert">여기 있는 내용</App>, document.getElementById('root'));
```

>기본 값 설정 - class 선언후  
Component.defaultProps = { ... }

``` react.js
class App extends React.Component {
    render() {
        return (
            <div> {this.props.value} </div>
        );
    }
};

App.defaultProps = {
    value:0
};
```


>Type 검증
Component.propTypes = { ... }

``` react.js
class App extends React.Component {
    render() {
        return (
            <div> 
                {this.props.value} 
                {this.props.secondValue}
                {this.props.thirdValue}
            </div>
        );
    }
};

App.propTypes = {
    value:React.PropTypes.string,
    secondValue:React.PropType.number,
    thirdValue:React.PropTypes.any.isRequired /*어떤 타입이던 필수 입력*/
};
```


>proptype 예제
``` react.js
class Codelab extends React.Component {
  render(){
     return (
      <div>
         <h1>hello</h1>
         <h1>Hello {this.props.name} </h1>
         <h2> {this.props.number}  </h2>
         <div>{this.props.children}</div>
      </div>
     );
  }
}

Codelab.propTypes = {
    name: React.PropTypes.string,
    number: React.PropTypes.number.isRequired
}

Codelab.defaultProps = {
  name:'UnKnown',
};


class App extends React.Component {
  render() {
    return (
      <Codelab name={this.props.name} number={this.props.number}>{this.props.children} </Codelab>  
    );
  }
}

ReactDOM.render(<App number={5}>여기 있는 내용</App>, document.getElementById('root'));


```



--------
### state
- 유동적인 데이터
- jsx내부에 {this.state.stateName}
- 초기값 설정이 필수, 생성자 (constructor) 에서 this.state = {} 으로 설정 
- 값을 수정할 때에는 this.setState({..}), 렌더링 된 다음엔 this.state = 절대 사용하지 말 것

``` react.js
class App extends React.Component {
  constructor(props) {
    super(props);
    this.state={
      value:0
    };
    this.handleClick = this.handleClick.bind(this);
  }
  
  handleClick() {
    this.setState({
      value:this.state.value + 1
    });
  }
  
  render() {
    return (
      <div>
        <h2>{this.state.value}</h2>
        <button onClick={this.handleClick}>Press me</button>
        </div>
    );
  }
};

ReactDOM.render(
  <App></App>,
  document.getElementById("root")
);

```


--------
### Component Mapping
>1. Map()
- 비슷한 코드를 반복해서 렌더링 
- 데이터 배열을 리엑트에선 JS 내장함수인 Map 을 사용 
- map() 메소드는 파라미터로 전달된 함수를 통하여 배열 내의 각 요소를 처리해서 그 결과로 새로운 배열을 생성함.

``` react.js
class Contactinfo extends React.Component {
  render() {
    return (
      <div>
        {this.props.contact.name}
        {this.props.contact.phone}
      </div>
    )
  }
};
class Contact extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      contactData:[
        {name:'abet', phone:'010-1234-1234'},
        {name:'bbbb', phone:'011-1234-1234'},
        {name:'cccc', phone:'012-1234-1234'},
        {name:'dddd', phone:'013-1234-1234'}
      ]
    }
  }
  
  render() {
    const mapToComponent = (data) => {
        return data.map((contact,i) => {
          return (<Contactinfo contact={contact} key={i}/>);
        });
    };
    
    return(
      <div>
        {mapToComponent(this.state.contactData)}
      </div>
    )
  }
};

class App extends React.Component {
  render() {
    return (
      <Contact/>
    );
  }
};

ReactDOM.render(
  <App></App>,
  document.getElementById("root")
);
  
```
--------
### 프로젝트 세팅
- webpack : 브라우저 위에서 import(require)를 할 수 있게 해주고 자바스크립트 파일들을 하나로 합쳐줌.
- webpack-dev-server : 별도의 서버를 구축하지 않고도 static 파일을 다루는 웹서버를 열 수 있으며 hot-loader를 통하여 코드가 수정될 때마다 자동으로 리로드 되게 할 수 있음.


``` cli
sudo npm install -g webpack webpack-dev-server

```


- webpack, webpack-cli error 
- webpack version 4부터 loader 대신 rules 로 사용 
``` javascript
    module: {
        rules: [
          {
            //query 대신 options
```


- npm run dev-server 실행이후 babel 관련 에러시  bable-core, babel-loader 버전 확인
``` cli
ERROR in ./src/index.js
Module build failed (from ./node_modules/babel-loader/lib/index.js):
Error: Cannot find module '@babel/core'
```
``` javascript
    "@babel/core": "^7.13.15",
    "babel-loader": "^8.2.2",
    // loader가 8이면 core 는 7로
``` 

--------
### 노마드코더 - movielist app
- async - await 비동기처리 ES7 문법
``` react.js
getMovies = async () => {
    const movies = await xios.get("https://yts-proxy.now.sh/list_movies.json");
  };
  asyccomponentDidMount(){
    this.getMovies();
  }
``` 

<img width="1402" alt="스크린샷 2021-04-20 오후 10 14 01" src="https://user-images.githubusercontent.com/48319693/115401797-bfc85900-a225-11eb-9aae-e663946406c9.png">

``` cli
npm start
``` 
