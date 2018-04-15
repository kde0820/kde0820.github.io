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
