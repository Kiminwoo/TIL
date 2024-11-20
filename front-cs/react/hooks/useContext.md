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

### context : 이전에 createContext 로 생성한 context 이며 정보를 보유하지 안흥며 , 컴포넌트에서 제공하거나 읽을 수 있는 정보의 종류를 나타냅니다.

