# useId

### 1. Что такое useId?

Хук `useId` позволяет создавать уникальные идентификаторы, которые затем можно использовать, например, в атрибутах доступности.
`useId` не принимает параметров, возвращает уникальный идентификатор, привязанный к данному конкретному вызову useId в данном конкретном компоненте. `useId` не должен использоваться для создания ключей в списках, ключи должны выбираться на основе данных.
