**1. 마운팅(Mounting) 단계**

컴포넌트가 생성되어 DOM에 삽입될 때 발생 

- constructor() : 컴포넌트가 처음 생성될 때 호출 

- static getDerivedStateFromProps() : 컴포넌트가 마운트되기 직전에 호출 

- render() : 컴포넌트의 JSX를 반환 후 렌더링

- componentDidMount() : 컴포넌트가 처음 렌더링된 후 호출

**2. 업데이트(Updating) 단계**

컴포넌트의 상태 또는 속성이 변경될 때마다 발생

- static getDerivedStateFromProps() : 새로운 props 들어올 때마다 호출 

- shouldComponentUpdate() : 컴포넌트가 리렌더링을 해야 하는지 여부 결정

- render() : 상태 or props 변경될 때 마다 호출 후 업데이트 UI 반환

- getSnapshotBeforeUpdate() - DOM 업데이트 되기 직전에 호출 

- componentDidUpdate() - 컴포넌트가 리렌더링되고 DOM 업데이트 후 호출 

**3. 언마운팅(Unmounting) 단계**

컴포넌트가 DOM에서 제거될 때 발생 