---
title: "setTimeout"
authors:
  - Windrushfarer
keywords:
  - таймаут
tags:
  - doka
---

## Кратко

`setTimeout` позволяет исполнить функцию через заданный промежуток времени. Метод возвращает числовой идентификатор установленного таймера. Этот идентификатор можно передать в метод [`clearTimeout`](/js/cleartimeout), чтобы остановить таймер.

## Как пишется

```js
const timerId = setTimeout(() => {
  console.log('Прошла 1 секунда')
}, 1000)

// Выведет число
console.log(timerId)
```

Пример выше установит таймер в 1 секунду и по истечении этого времени сработает функция, которая выведет в консоль сообщение.

`setTimeout` принимает два аргумента:
- функция, которая выполнится когда таймер закончится. В переданная функцию не передаются никакие параметры
- время таймера в миллисекундах

:::callout ⏱

Миллисекунда – это одна тысячная доля секунды, то есть одна секунда состоит из 1000 миллисекунд.

:::

В результате вызова `setTimeout` вернёт идентификатор установленного таймера.

## Как понять

В JavaScript код выполняется [по порядку сверху вниз](/js/execution-order). Если интерпретатор встречает вызов функции, то он сразу выполняет её. Но разработчику часто может понадобится запланировать вызов функции, чтобы она выполнилась не сразу.

Запланировать одноразовое выполнение функции можно как раз с помощью `setTimeout`. Это самый простой способ исполнить функцию [асинхронно](/js/async-in-js).

Время таймера не гарантирует, что функция будет выполнена точно в момент, когда таймер закончится. Таймер ждёт, пока выполнится синхронный код и только потом запускает отложенную функцию, если время истекло. Строго говоря, когда мы устанавливаем таймаут, то нужно ожидать, что функция выполнится в произвольный момент после указанного времени.

<iframe title="Неточное выполнение отложенной функции через setTimeout" src="demos/index.html" height="300"></iframe>

Таймауты всегда имеют свой числовой идентификатор, он хранится в браузере в [списке активных таймеров](https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#list-of-active-timers). Этот идентификатор нужно использовать, если необходимо очистить таймаут.

Таймауты часто применяются для выпадающих списков или тултипов, чтобы закрывать их с небольшой задержкой. Только с помощью таймаутов можно создать такую полезную функцию как [`debounce`](/js/debounce).