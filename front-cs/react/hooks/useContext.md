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

