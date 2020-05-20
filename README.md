# React Hooks

Created: May 20, 2020 11:15 PM

functional component 에서 state 를 갖을 수 있게 해준다. ComponentDidMount() 등을 사용하지 않아도 된다. Functional Programming 을 사용 할 수 있게 해준다.

```tsx
import React, { useState } from "react";
import "./styles.css";

const App = () => {
  const [item, setItem] = useState(1);
  const incrementItem = () => setItem(item + 1);
  const decrementItem = () => setItem(item - 1);
  return (
    <div className="App">
      <h1>Hello {item}</h1>
      <h2>Start editing to see some magic happen!</h2>
      <button onClick={incrementItem}>Increment</button>
      <button onClick={decrementItem}>Decrement</button>
    </div>
  );
};

export default App;
```

`this.state.item` 이렇게 값에 접근 할 필요 없고. `this.setState({item: 1})` 로 수정해 줄 필요가 없다.

# 분리된 엔티티에서 이벤트 처리

```tsx
const useInput = initialValue => {
  const [value, setValue] = useState(initialValue);
  const onChange = event => {
    console.log(event.target);
  };
  return { value, onChange };
};

const App = () => {
  const name = useInput("Mr.");
  return (
    <div className="App">
      <h1>Hello</h1>
      <input placeholder="Name" {...name} />
    </div>
  );
};

export default App;
```

상태 관리하는 것을 다른 부분으로 함수로 분리 할 수 있고, 다른 파일로 또한 분리 할 수 있다.

## validator

```tsx
const useInput = (initialValue, validator) => {
  const [value, setValue] = useState(initialValue);
  const onChange = event => {
    const {
      target: { value }
    } = event;
    let willUpdate = true;
    if (typeof validator === "function") {
      willUpdate = validator(value);
    }
    if (willUpdate) {
      setValue(value);
    }
  };
  return { value, onChange };
};
```
