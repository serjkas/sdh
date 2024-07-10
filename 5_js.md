# JS

## Изначально JavaScript был создан, чтобы «сделать веб-страницы живыми»

Сегодня JavaScript может выполняться не только в браузере, но и на сервере или на любом другом устройстве, которое имеет специальную программу, называющуюся «движком» JavaScript.

## Чего НЕ может JavaScript в браузере?

- javavaScript на веб-странице не может читать/записывать произвольные файлы на жёстком диске, копировать их или запускать программы. Он не имеет прямого доступа к системным функциям ОС.
- Различные окна/вкладки не знают друг о друге.
- JavaScript может легко взаимодействовать с сервером, с которого пришла текущая страница. Но его способность получать данные с других сайтов/доменов ограничена.

## Языки «над» JavaScript

Есть много чего, от CoffeeScript до Brython

Нас тут итересует Typescript

- TypeScript концентрируется на добавлении «строгой типизации» для упрощения разработки и поддержки больших и сложных систем

## Основы js

### Объявление переменных

- const
- let
- var (устарело)

### Типы данных

#### Примитивы

- number для любых чисел: целочисленных или чисел с плавающей точкой; целочисленные значения ограничены диапазоном ±(253-1).
- bigint для целых чисел произвольной длины.
- string для строк. Строка может содержать ноль или больше символов, нет отдельного символьного типа.
- boolean для true/false.
- null для неизвестных значений – отдельный тип, имеющий одно   значение null.
- undefined для неприсвоенных значений – отдельный тип, имеющий одно значение undefined.
- symbol для уникальных идентификаторов.

#### Не Примитивы

- object почти все чтоне является примитивами является объектом, в том числе и функции

### Преобразование типов

- Number() или + перед переменной
- String() или `` или .toString()
- Boolean() или !!, одинарный ! для отрицания, всегда отдаст так же булеан

### Базовые операторы

- Сложение +
- Вычитание -
- Умножение *
- Деление /

### Операторы сравнения

- \> больше, меньше
- < больше, меньше
- == сравнение не строгое
- === сравнение строгое
- ||
    Используйте || если вам нужно вернуть первое "истинное" (truthy) значение или в случае необходимости обработать любое falsy значение как одинаковое (например, когда '', 0, false должны быть обработаны одинаково).
- ??
    Используйте ??, когда вам важно обрабатывать только null или undefined и сохранять другие falsy значения, такие как 0, false, и '' (пустая строка). Это особенно полезно для задания значений по умолчанию, которые могут допускать "ложные" значения в качестве валидных.

### Ветвление

- if

    ```js
    if (a === 'B') {

    }
    ```

- else

    ```js
    if (a === 'A') {

    } else {
        
    }
    ```

- if else

    ```js
    if (a === 'A') {

    } else if (a === 'A') {
        
    } else {}
    ```

- Условный оператор **?**

    ```js
    let result = условие ? значение1 : значение2
    ```

### циклы

#### break, continue

- do while

    ```js
    do {
  // тело цикла
    } while (condition);

    ```

- while

  ```js
  let i = 3;

    while (i) { // когда i будет равно 0, условие станет ложным, и цикл остановится
        alert( i );
        i--;
    }
  ```

- for
  - for  (начало; условие; шаг)

    ```js
    for (let i = 0; i < 3; i++) { // выведет 0, затем 1, затем 2
        alert(i);
    }
    ```

  - for of для  итерируемых объектов

    ```js
    for (variable of iterable) {
        statement
    }
    ```

### Функции

```js
function showMessage(a, b = 2) {
    console.log(a)
    alert( 'Всем привет!' );
}
```

```js
const func1 = (arg1, arg2, ...argN) => expression;

const sum = (a, b) => {  
  let result = a + b;
  return result; 
};
```

### Spread / Rest

- spread это конструкция в JavaScript, которая позволяет передавать элементы массива или свойства объекта в виде отдельных аргументов.
- rest — это синтаксическая конструкция в JavaScript, которая позволяет собирать оставшиеся элементы массива в другой массив или собирать оставшиеся свойства объекта в другой объект

  > Когда синтаксис ... используется для «распаковки» элементов массива или объекта в отдельные аргументы — это spread. А если три точки используются для сбора оставшихся аргументов в массив или объект — это оператор rest.

### Работа с массивами

- arr.push(...items) – добавляет элементы в конец,
- arr.pop() – извлекает элемент из конца,
- arr.shift() – извлекает элемент из начала,
- arr.unshift(...items) – добавляет элементы в начало
- arr.splice(start[, deleteCount, elem1, ..., elemN]) удаление элемента из массива
- arr.slice([start], [end]) - Он возвращает новый массив, в который копирует все элементы с индекса start до end (не включая end).
- arr.forEach(function(item, index, array) {
        // ... делать что-то с item
    });
- [1, 2, 3].includes(2); // true
- arr.indexOf(searchElement[, fromIndex = 0])
- arr.find(item => item.id == 1);
- arr.filter(item => item.id < 3) - возвращает новый массив

- arr.map(item => {
   return {
    a: item.id,
    b: item.name
   }
  }) - возвращает новый массив

-

#### Функции-«колбэки»

```js
function ask(question, yes, no) {
  if (confirm(question)) {
    yes()
    }
  else {
    no()
    };
}

function showOk() {
  alert( "Вы согласны." );
}

function showCancel() {
  alert( "Вы отменили выполнение." );
}

ask("Вы согласны?", showOk, showCancel);


```

### Promise

[урок](https://learn.javascript.ru/promise)

способ организации асинхронного кода

> Promise – это специальный объект, который содержит своё состояние. Вначале `pending` («ожидание»), затем – одно из: `fulfilled` («выполнено успешно») или `rejected` («выполнено с ошибкой»).

- Код, которому надо сделать что-то асинхронно, создаёт объект promise и возвращает его.
- Внешний код, получив promise, навешивает на него обработчики.
- По завершении процесса асинхронный код переводит promise в состояние fulfilled (с результатом) или rejected (с ошибкой). При этом автоматически вызываются соответствующие обработчики во внешнем коде.

#### Создание промиса

```js
var promise = new Promise(function(resolve, reject) {
  // Эта функция будет вызвана автоматически

  // В ней можно делать любые асинхронные операции,
  // А когда они завершатся — нужно вызвать одно из:
  // resolve(результат) при успешном выполнении
  // reject(ошибка) при ошибке
  
})
```

#### Универсальный метод для навешивания обработчиков

```js
promise.then(onFulfilled, onRejected)
promise.catch()
```

## Async/await

специальный синтаксис для работы с промисами

```js
async function f() {

  try {
    let response = await fetch('/no-user-here');
    let user = await response.json();
  } catch(err) {
    // перехватит любую ошибку в блоке try: и в fetch, и в response.json
    alert(err);
  }
}

f();
```

## ДЗ

### Обработка данных

получить данные с <https://jsonplaceholder.typicode.com/>
с раздела posts и вывести данные в консоль, либо в html без ключей userId
**Если нет доступа то берем Json ниже как пример**
пример, получили:
> [
  {
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
  },
  {
    "userId": 1,
    "id": 2,
    "title": "qui est esse",
    "body": "est rerum tempore vitae\nsequi sint nihil reprehenderit dolor beatae ea dolores neque\nfugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis\nqui aperiam non debitis possimus qui neque nisi nulla"
  },
  {
    "userId": 1,
    "id": 3,
    "title": "ea molestias quasi exercitationem repellat qui ipsa sit aut",
    "body": "et iusto sed quo iure\nvoluptatem occaecati omnis eligendi aut ad\nvoluptatem doloribus vel accusantium quis pariatur\nmolestiae porro eius odio et labore et velit aut"
  }]  

пример, вывели:
> [{
    "id": 3,
    "title": "ea molestias quasi exercitationem repellat qui ipsa sit aut",
    "body": "et iusto sed quo iure\nvoluptatem occaecati omnis eligendi aut ad\nvoluptatem doloribus vel accusantium quis pariatur\nmolestiae porro eius odio et labore et velit aut"
  }]

### Проверка на пустой объект / массив

Если задан объект или массив, вернуть значение, если он пуст.
- Пустой объект не содержит пар ключ-значение.
- Пустой массив не содержит элементов.

[урок](https://leetcode.com/problems/is-object-empty/?envType=study-plan-v2&envId=30-days-of-javascript)

### Возврат длины переданных аргументов
Напишите функцию  argumentsLength, которая возвращает количество переданных ей аргументов.

[урок](https://leetcode.com/problems/return-length-of-arguments-passed/?envType=study-plan-v2&envId=30-days-of-javascript)
