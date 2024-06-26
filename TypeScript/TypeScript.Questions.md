# TypeScript

### 1. Что такое TypeScript и для чего он используется?

Это надмножество JavaScript (JS), среди основных особенностей которого можно отметить возможность явного статического назначения типов, поддержку классов и интерфейсов. Предоставляет дополнительные возможности типизации и статического анализа кода. Он используется для разработки сложных приложений, где необходимо обеспечить безопасность и надежность кода.

### 2. Обобщенные типы в TypeScript

Обобщённые типы (generics) позволяют создавать компоненты или функции, которые могут работать с различными типами, а не с каким-то одним.

### 3. Виды типизации

- **Статическая** - тип связывается с переменной в момент ее объявления. Тип переменной неизменяемый.
- **Динамическая** - тип связывается с переменной в момент попадания в нее значения. Тип изменяемый.

Язык JavaScript с динамической типизацией, допускающий в процессе разработки послабления, ведущие к ошибкам. Например сложение числа и строки не вызовет ошибки. Для решения проблемы были разработаны инструменты статической типизации:

- **PropTypes** - предназначен для приложений на React. Легкий, обозначает простые типы, подходит для маленьких проектов.
- **Flow** - разработан Facebook. Считается более производительным за счет того, что не требует компиляции.
- **TypeScript** - разработан Microsoft. Имеет богатую экосистему библиотек, легкочитаем.

![alt text](/assets/JSmeme.png)
