---
layout: post
title: React Study
comments: true
---
inflearn 강좌 "React & Express를 이용한 웹 어플리케이션 개발하기"를 수강하며 공부한 내용입니다.

## React.js
- Virtual DOM
- component들로 구성

> 장점

- 배우기 쉽다
- Garbage Collection, 메모리 관리, 성능
- 서버 & 클라이언트 렌더링
- 다른 프레임워크나 라이브러리와 혼용가능

> 단점

- VIEW ONLY
- IE8 이하 지원 X

> React 기본 구조
```
class Codelab extends React.component {
  render(){
    return(
      <div>Codelab</div>
     );
  }
}

class App extends React.component {
  render(){
    return(
      <Codelab/>
     );
  }
}

ReactDOM.render(<App/>, document.getElementById('root'));
```

## Props
- 변동되지 않는 데이터
```
class Codelab extends React.component {
  render(){
    return(
      <div>
        <h1>Hello {this.props.name}</h1>
        <div>{this.props.children}</div>
      </div>
     );
  }
}

class App extends React.component {
  render(){
    return(
      <Codelab name="velopert">여기 있는 내용</Codelab>
     );
  }
}

ReactDOM.render(<App/>, document.getElementById("root"));
```

## State
- 유동적인 데이터
- 초기값 설정 필수 생성자에서 this.state = {} 으로 설정

```
class Counter extends React.Component {
  
  /* 생성자 */
  constructor(props){
    super(props);
    /* state 초기값 설정 */
    this.state = {
      value: 0
    };
    /* 이거 안해주면 작동 X */
    this.handleClick = this.handleClick.bind(this)
  }
  
  handleClick(){
    this.setState({
      value: this.state.value + 1
    });
  }
  
  render() {
    return(
      <div>
        <h2>{this.state.value}</h2>
        <button onClick={this.handleClick}>Press Me</button>
      </div>
    );
  }
}

class App extends React.Component {
  render() {
    return(
      <Counter/>
    );
  }
}

ReactDOM.render(<App/>, document.getElementById('root'));
```

## Component Mapping
- javascript Map 사용
- map() : 파라미터로 전달된 함수를 통하여 배열 내의 각 요소를 처리해서 그 결과로 새로운 배열을 생성함

```
class Contactinfo extends React.Component {
  render() {
    return(
      <div>{this.props.contact.name}  {this.props.contact.phone}</div>
    );
  }
}

class Contact extends React.Component {
  
  constructor(props){
    super(props);
    this.state = {
      contactData: [
        {name: 'Albert', phone: '010-0000-0001'},
        {name: 'Albert2', phone: '010-0000-0002'},
        {name: 'Albert3', phone: '010-0000-0003'},
        {name: 'Albert4', phone: '010-0000-0004'}
      ]
    }
  }
  render() {
    /* 상수 */
    const mapToComponent = (data) => {
        return data.map((contact,i) => {
          return (<Contactinfo contact={contact} key={i}/>);
        });
    };
    
    
    return(
      <div>
        {mapToComponent(this.state.contactData)}
      </div>
    );
  }
}

class App extends React.Component {
  render() {
    return(
      <Contact/>
    );
  }
}

ReactDOM.render(<App/>, document.getElementById('root'));
```