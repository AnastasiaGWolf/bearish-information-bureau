## Задачи на использование useState
### Задача 1.
Есть классовый компонент с состоянием. Каждый раз, когда нажимается кнопка в компоненте, счетчик увеличивается. Необходимо переписать компонент с использованием хука.
```javascript
class Counter extends Component {
    state = {
        count: 0,
    };

    incrementCount = () => {
        this.setState({
            count: this.state.count + 1,
        });
    };

    render() {
        return (
            <div>
            <button onClick={this.incrementCount}>Count: {this.state.count}</button>
        </div>
    	);
    }
}
```
__Решение__
```javascript
import React, { useState } from "react";
function Counter() {
    const [count, setCount] = useState(0);
return (
        <div>
            <button type="button" onClick={() => { setCount(count + 1) }} >
                Count: {count}
            </button>
        </div>
    );
}
```

### Задача 2.
Есть классовый компонент. Он содержит код для обновления состояния на основе предыдущего значения состояния. Необходимо переписать код, используя хуки React.
```javascript
class Counter extends Component {
    state = { count: 0 };

    incrementCount = () => {
        this.setState((prevState) => {
            return { count: prevState.count + 1 };
        });
    };

    decrementCount = () => {
        this.setState((prevState) => {
            return { count: prevState.count - 1 };
        });
    };

    render() {
        return (
            <div>
                <strong>Count: {this.state.count}</strong>
                <button onClick={this.incrementCount}>Increment</button>
                <button onClick={this.decrementCount}>Decrement</button>
            </div>
        );
    }
}
```
__Решение:__  
Можно обновить значение переменной состояния, просто передав новое значение в функцию обновления или передав callback. Второй способ с передачей callback-функции безопасен в использовании.
```javascript
import React, { useState } from "react";

function Counter() {
    const [count, setCount] = useState(0);

    const incrementCount = () => {
        setCount((prevCount) => {
            return prevCount + 1;
        });
    };

    const decrementCount = () => {
        setCount((prevCount) => {
            return prevCount - 1;
        });
    };

    return (
        <div>
            <strong>Count: {count}</strong>
            <button onClick={incrementCount}>Increment</button>
            <button onClick={decrementCount}>Decrement</button>
        </div>
    );
}
```
### Задача 3.
Есть классовый компонент, который обновляет состояние, используя ввод из формы. Необходимо переписать код, используя хуки React.

```javascript
export class Profile extends Component {
    state = {
        name: "Backbencher",
        age: 23,
    };

    onNameChange = (e) => {
        this.setState({
            name: e.target.value,
        });
    };

    onAgeChange = (e) => {
        this.setState({
            age: e.target.value,
        });
    };

    render() {
        return (
            <div>
                <form>
                    <input
                        type="text"
                        value={this.state.name}
                        onChange={this.onNameChange}
                    />
                    <input
                        type="number"
                        value={this.state.age}
                        onChange={this.onAgeChange}
                    />
                    <h2>
                        Name: {this.state.name}, Age: {this.state.age}
                    </h2>
                </form>
            </div>
        );
    }
}
```
__Решение:__  
Функция обновления состояния в useState() не выполняет автоматическое слияние, если в состоянии хранится объект. Но в случае использования метода setState() в классовых компонентах происходит автоматическое слияние.
Здесь мы объединяем свойства объекта с помощью spread оператора JavaScript.

```javascript
import React, { useState } from "react";

function Profile() {
    const [profile, setProfile] = useState({
        name: "Backbencher",
        age: 23,
    });

    const onNameChange = (e) => {
        setProfile({ ...profile, name: e.target.value });
    };

    const onAgeChange = (e) => {
        setProfile({ ...profile, age: e.target.value });
    };

    return (
        <div>
            <form>
                <input type="text" value={profile.name} onChange={onNameChange} />
                <input type="text" value={profile.age} onChange={onAgeChange} />
                <h2>
                    Name: {profile.name}, Age: {profile.age}
                </h2>
            </form>
        </div>
    );
}
```