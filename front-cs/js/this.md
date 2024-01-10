# this의 용법

## this는 호출 패턴에 따라 다른 객체를 참조. 실행 컨텍스트가 생성될 때마다 this의 바인딩이 일어나며 우선순위 순으로 나열

1. new 를 사용했을 때 해당 객체로 바인딩됨

````Javascript

    var name = 'global';

    function Func() {
        this.name = 'Func';
        this.print = function f() {
            console.log(this.name);
        };
    }

    var a = new Func();
    a.print(); // Func


````

2. call,apply,bind 와 같은 명시적 바인딩을 사용했을 때 인자로 전달된 객체에 바인딩됨

````Javascript

    function func() {
        console.log(this.name);
    }

    var obj = { name: 'obj name' };

    func.call(obj); // obj name
    func.apply(obj); // obj name
    func.bind(obj)(); // obj name


````

3. **객체**의 메소드로 호출할 경우 해당 객체에 바인딩됨

````Javascript

    var obj = {
        name: 'obj name',
        print: function p() {
            console.log(this.name);
        },
    };

    obj.print(); // obj name


````

4. 그 외의 경우

- strict mode(엄격모드) : undefined 로 초기화
- 일반 : 브라우저라면 window 객체에 바인딩


## 바인딩

- 프로그램의 어떤 기본 단위가 가질 수 있는 구성요소의 구체적인 값, 성격을 확정하는 것을 말함.

## EC 

- 실행 컨텍스트(Execution Context) , scope , hoisting , this , function , closure 등의 동작 원리를 담고 있는 자바스크립트 핵심원리

## new

- 사용자 정의 객체 타입 or 내장 객체 타입의 인스턴스를 생성 

## call

- 함수를 실행하고 함수의 첫 번째 인자로 전달하는 값에 this를 바인딩.

## apply 

- 함수를 실행하고 함수의 첫 번째 인자로 전달하는 값에 this를 바인딩. 
- call과 차이점은 인자를 배열의 형태로 전달한다는 것. 이 때 인자로 배열 자체가 전달되는 것이 아니라 , 배열의 요소들이 값으로 전달됨

## bind 

- 함수의 첫 번째 인자에 this를 바인딩. 그러나 함수를 실행하지 않으며 새로운 함수를 반환. 반환된 새로운 함수를 실행해야 원본 함수가 실행됨.
