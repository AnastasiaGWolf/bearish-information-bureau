# useReduser

### 1. Что такое useReducer? *(кратко)*

хук, позволяющий управлять состоянием компонента с помощью
функции-редюсера.

### 2. Что принимает в себя useReducer, что возвращает? *(кратко)*
Принимает:
1. Функция редюсера которое принимает два аргумента: текущее состояние и действие, и возвращает новое состояние.  
2. Начальное состояние компонента до любых изменений.

Возвращает массив с двумя элементами:
1. Текущее состояние компонента, которое может изменяться в ответ на действия.
2. dispatch функция для отправки действий (actions) в редюсер


### 3. Что такое reducer в Redux и какие параметры он принимает?

Reducer – это чистая функция, принимающая в качестве параметров состояние и действие. Внутри reducer мы отслеживаем тип полученного действия и, в зависимости от него, модифицируем состояние и возвращаем новый объект состояния.

```javascript
export default function appReducer(state = initialState, action) {
  // reducer смотрит на тип action и решает какое действие совершать
  switch (action.type) {
    // Описываются case'ы для каждого типа action
    default:
      // Если reducer не нашел ни одного подходящего типа action, то здесь возвращается текущее состояние без изменений
      return state
  }
}
```

### 4. Что такое действие и как можно изменить состояние в Redux?

Действие – это простой объект JavaScript, который должен иметь поле с типом:
```javascript
{
  type: 'SOME_TYPE'
}
```

Опционально в качестве полезной нагрузки (payload) можно добавить какие-нибудь данные. Чтобы изменить состояние, необходимо вызвать функцию диспетчеризации и передать ей действие:
```javascript
{
  type: 'SOME_TYPE'
  payload: 'Any payload',
}
```
