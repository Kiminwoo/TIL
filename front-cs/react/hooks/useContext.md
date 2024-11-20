# react@18.2.0

# **useContext**

```javascript
const value = useContext(SomeContext);
```

### **컴포넌트의 최상위 레벨에서 useContext 를 호출하여 context를 읽고 구독합니다.**

```javascript
import {useContext} from 'react';

function MyComponent(){
    const theme = useContext(ThemeContext);
}
// ... 
```

### 매개변수
> context : 이전에 createContext 로 생성한 context 이며 정보를 보유하지 안흥며 , 컴포넌트에서 제공하거나 읽을 수 있는 정보의 종류를 나타냅니다. 

### 반환값

> useContext 는 호출하는 컴포넌트에 대한 context 값을 반환. 이 값은 호출한 컴포넌트에서 트리상 위에 있는 가장 가까운 SomeContext.Provider 에 전달된 value. react 는 context가 변경되면 context 를 읽는 컴포넌트를 자동으로 리렌더링 합니다.


### 주의사항

> 컴포넌트의 useContext() 호출은 동일한 컴포넌트에서 반환된 provider 영향을 받지 않습니다. 해당 <Context.Provider> 는 반드시 useContext() 호출을 수행하는 **컴포넌트의** 위에 있어야 합니다.

> react 는 변경된 value 를 받는 provider 부터 시작해서 해당 context를 사용하는 자식들에 대해서까지 전부 자동으로 **리렌더링** 합니다. 이전 값과 다음 값은 Object.is 로 비교합니다. memo로 리렌더링을 건너뛰어도 새로운 context 값을 수신하는 자식들을 막지는 못합니다.


> 빌드 시스템이 출력 결과에 중복 모듈을 생성하는 경우 (심볼릭 링크를 사용하는 경우 발생할 수 있음) context가 손상될 수 있습니다. context 를 통해 무언가를 전달하는 것은 === 비교에 의해 결정되는 것처럼 context를 제공하는 데 사용하는 SomeContext 와 context 를 읽는 데 사용하는 SomeContext 가 **정확하게 동일한 객체** 인 경우에만 작동합니다.


### 사용법

> 컴포넌트의 최상위 레벨에서 useContext 를 호출하여 `context` 를 읽고 구독합니다.

```javascript

import { useContext } from 'react';

function Button(){
    const theme = useContext(ThemeContext);
}

```

> `useContext` 는 전달한 context에 대한 context 값을 반환합니다. context 값을 결정하기 위해 react 는 컴포넌트 트리를 검색하고 특정 context 에 대해 **위에서 가장 가까운 context provider** 를 찹습니다.

> context 를 `Button` 에 전달하려면 해당 버튼 또는 상위 컴포넌트 중 하나를 해당 context provider 로 감쌉니다.

```javascript
function MyPage(){
    return (
        <ThemeContext.Provider value="dark">
            <Form />
        </ThemeContext.Provider>
    )
}

function Form(){
    // .... renders buttons inside ....
}

```

> provider 와 `Button` 사이에 얼마나 많은 컴포넌트 레이어가 있는지는 중요하지 않습니다. Form 내부의 `Button` 이 `useContext(ThemeContext)` 를 호출하면 `"dark"` 를 값으로 받습니다.

### ❗️주의사항❗️ 

> useContext() 는 항상 그것을 호출하는 컴포넌트 위의 가장 가까운 provider를 찾습니다. 호출하는 컴포넌트 내의 provider는 고려하지 않습니다.


### context를 통해 전달된 데이터 업데이트하기

> context 를 업데이트하려면 state와 결합해야 합니다. 부모 컴포넌트에 state 변수를 선언하고 현재 state를 context 값 으로 provider 에 전달합니다.

```javascript
function MyPage(){
    const [theme , setTheme] = useState('dark');
    return (
        <ThemeContext.Provider value={theme}>
            <Form />
            <Button onClick={()=>{
                setTheme('light');
            }}>
            
            Switch to light theme
            </Button>
            
        </ThemeContext.Provider>
    );
}
```

> provider 내부의 모든 `Button` 은 현재 theme 값을 받게 됩니다. provider 에게 전달한 theme 값을 업데이트하기 위해 setTheme 를 호출하면 모든 Button 컴포넌트가 새로운 light 값으로 리렌더링됩니다.

> JSX 중괄호를 사용하여 javascript theme 변수 값을 전달합니다. 중괄호를 사용하면 문자열이 아닌 context 값도 전달할 수 있습니다.

### fallback 기본값 지정하기

> react 가 부모 트리에서 특정 context 의 provider 들을 찾을 수 없는 경우 , useContext() 가 반환하는 context 값은 해당 context 를 생성할 때 지정한 기본값과 동일합니다.

```javascript
const ThemeContext = createContext(null);
```
> 기본값은 절대 변경되지 않습니다. context를 업데이트하려면 앞서 설명된 대로 state를 사용하세요

> null 대신 기본값으로 사용할 수 있는 더 의미있는 값이 있는 경우가 많습니다.

```javascript
const ThemeContext = createContext('light');
```

> 이렇게 하면 실수로 해당 provider 없이 일부 컴포넌트를 렌더링해도 중단되지 않습니다. 또한 테스트 환경에서 많은 provider 를 설정하지 않고도 테스트 환경에서 잘 작동하는 데 도움이 됩니다.

> 아래 예시에서 '테마 전환' 버튼은 테마 **context provider 외부에 있고 ** 기본 context 테마 값이 'light' 이므로 항상 밝게 표시됩니다. 


### 트리 일부에 대한 context 재정의하기

> 트리의 일부분을 다른 값의 provider로 감싸 해당 부분에 대한 context를 재정의할 수 있습니다.