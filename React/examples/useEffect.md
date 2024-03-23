## Задачи на использование useEffect
### Задача 1.
Есть классовый компонент, который печатает _Boom_ в консоли каждый раз, когда он монтируется или обновляется. Необходимо удалить избыточные выражения console.log с помощью хуков React.

```javascript
export class Banner extends Component {
    state = {
        count: 0,
    };

    updateState = () => {
        this.setState({
            count: this.state.count + 1,
        });
    };

    componentDidMount() {
        console.log("Boom");
    }

    componentDidUpdate() {
        console.log("Boom");
    }

    render() {
        return (
            <div>
                <button onClick={this.updateState}>State: {this.state.count}</button>
            </div>
        );
    }
}
```
__Решение__  
componentDidMount() и componentDidUpdate() - это методы жизненного цикла. Такие побочные эффекты можно сделать с помощью хука useEffect. Хук useEffect - это функция, которая принимает callback. Этот callback вызывается каждый раз, когда происходит рендеринг.

```javascript
import React, { useState, useEffect } from "react";

function Banner() {
    const [count, setCount] = useState(0);

    useEffect(() => {
        console.log("Boom");
    });

    const updateState = () => {
        setCount(count + 1);
    };

    return (
        <div>
            <button onClick={updateState}>State: {count}</button>
        </div>
    );
}
```
### Задача 2.
Код печатает сообщение «Счетчик обновлен» даже при обновлении значения в текстовом поле. Как мы можем отображать сообщение только при обновлении состояния счетчика?

```javascript
function Banner() {
    const [count, setCount] = useState(0);
    const [name, setName] = useState("");

    useEffect(() => {
        console.log("Счетчик обновлен");
    });

    return (
        <div>
            <button onClick={() => setCount(count + 1)}>State: {count}</button>
            <input
                type="text"
                value={name}
                onChange={(e) => setName(e.target.value)}
            />
        </div>
    );
}
```
__Решение__  
Функция useEffect принимает второй параметр, который должен быть массивом. В этом массиве нам нужно передать props или состояние, за которым нам нужно следить. Эффект выполняется только в том случае, если эти свойства или состояние, упомянутые в массиве, изменяются. Поэтому в нашем коде мы добавляем второй аргумент и указываем только значение count в массиве.

```javascript
useEffect(() => {
    console.log("Count is updated");
}, [count]);
```