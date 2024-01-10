# 자바스크립트 동작 원리 (이벤트 루트)

![event-loop](https://github.com/Kiminwoo/front-cs/blob/main/img/javascript-eventloop.gif)

- 일반적인 작업은 콜스택(call stack)에서 이루어짐
- 시간이 소요되는 작업들(setTimeOut, 이벤트 , HTTP 요청 메서드 등)은 WebAPI애서 대기하다가 콜백큐(callback queue)로 보내짐
- call stack 이 비워져 있을때만 callback queue에 저장되어 있던 작업들을 call stack으로 보냄.

### 이벤트 루프 

-콜 스택이 다 비워지면 콜백 큐에 존재하는 함수를 하나씩 콜스택으로 옮기는 역할

### 콜스택

- 콜스택은 실행된 코드의 환경을 저장하는 자료구조로, 함수 호출 시 이곳에 저장이 됨. 어떤 하수를 저장하면 스택에 쌓고 또 다른 함수를 호출하면 그 다음 스택에 쌓이면서 가장 위에 쌓인 함수를 가장 먼저 처리(LIFO)

### WebAPI

- Web API는 브라우저에서 제공하는 API로 DOM, Ajax, TimeOut 등이 있습니다. 콜스택에서 실행된 비동기 함수는 Web API를 호출하고 , Web API는 콜백 함수를 task queue에 넣습니다.

### 콜백큐

- 콜백큐는 함수를 저장하는 자료구조로 , 콜스택과 다르게 가장 먼저 들어온 함수를 가장 먼저 처리 (FIFO)