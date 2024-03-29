# Примеры кастомных хуков

### Пользовательский хук `useLocalStorage`

```javascript
import { useEffect, useState } from 'react';

function getSavedValue(key: string, defaultValue: any): any {
  const savedValue = localStorage.getItem(key);
  return JSON.parse(savedValue) || defaultValue;
}

function useLocalStorage(key: string, initialValue: any): [any, (value: any) => void] {
  const [value, setValue] = useState(getSavedValue(key, initialValue));
  useEffect(() => localStorage.setItem(key, JSON.stringify(value)), [key, value]);
  return [value, setValue];
}

export default useLocalStorage;
```

1. `getSavedValue` - используется для получения сохраненного значения из локального хранилища по ключу. Если значение существует, оно будет преобразовано из строки JSON в объект JavaScript и возвращено. 
2. Хук возвращает массив, содержащий текущее значение состояния value и функцию setValue, которая используется для обновления состояния. Это позволяет легко использовать этот хук в компонентах и управлять значениями, хранящимися в локальном хранилище.

Пример использования:

```javascript
import React from 'react';
import useLocalStorage from './useLocalStorage';

function Home() {
  const [name, setName] = useLocalStorage('name', 'John');

  return (
    <div>
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <p>Hello, {name}!</p>
    </div>
  );
}
```

### Пользовательский хук для получения картинки собаки от внешней API

```javascript
import { useState, useEffect } from 'react';

const initState = {
    dog: '',
    isLoading: true
}

function useDog() {
const [dog, setDog] = useState(initState)

    const getDog = async () => {
        try {
            const response = await fetch('https://dog.ceo/api/breeds/image/random')
            const result = await response.json()
            setDog((prev) => ({ ...prev, dog: result.message, isLoading: false}))
        } catch (error) {
            console.log(error);
        }
    }

    useEffect(() => {
        getDog().catch((err) => err)
    }, [])

    return [dog, getDog]
}

export default useDog;
```

1. `initState`: Это объект, представляющий начальное состояние. Он содержит два поля: `dog`, представляющее URL изображения собаки, и `isLoading`, указывающее на текущее состояние загрузки.
2. Хук возвращает массив, содержащий текущее состояние `dog` и функцию `getDog`, которая используется для получения нового изображения собаки.

Пример использования:

```javascript
import React from 'react';
import useDog from '../../hooks/useDog';

export default function Dog(): JSX.Element {
  const [dog, getDog] = useDog();

  return (
    <section>
      {dog.isLoading ? (
        <h1>LOADING</h1>
      ) : (
        <div>
          <img src={dog.dog} alt="dog" style={{ height: '200px', width: '200px' }} />
          <br />
          <button type="button" onClick={getDog}>
            Дай собаку
          </button>
        </div>
      )}
    </section>
  );
}
```
