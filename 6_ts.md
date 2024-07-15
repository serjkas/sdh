# TS

## Интерфейсы (Interface)

Интерфейсы в TypeScript используются для определения структуры объекта. Они позволяют описывать, какие свойства и методы должен иметь объект.

Пример использования интерфейсов:

```ts
interface User {
  id: number;
  name: string;
  email: string;
}

const user: User = {
  id: 1,
  name: 'John Doe',
  email: 'john.doe@example.com'
};

function getUserInfo(user: User): string {
  return `User Info: ${user.name}, ${user.email}`;
}

console.log(getUserInfo(user)); // User Info: John Doe, john.doe@example.
```

## Типы (Type)

Типы в TypeScript позволяют определять не только структуры объектов, но и объединения (union), пересечения (intersection), алиасы типов и другие конструкции.
Примеры использования типов:

```ts
// Определение алиаса типа
type ID = number | string;

let userId: ID;
userId = 123; // ОК
userId = 'ABC'; // ОК

// Определение структуры объекта через тип
type Product = {
  id: number;
  name: string;
  price: number;
}

const product: Product = {
  id: 101,
  name: 'Laptop',
  price: 1500
};
```

## Основные различия

- Расширение (Extension)
Интерфейсы могут расширять (extend) другие интерфейсы и типы.
Типы могут объединяться (intersection) с другими типами и интерфейсами.

```ts
interface Person {
  name: string;
}

interface Employee extends Person {
  position: string;
}

type Animal = {
  species: string;
};

type Dog = Animal & {
  breed: string;
};
```

- Объединение (Declaration Merging)
Интерфейсы поддерживают объединение объявлений (declaration merging), что позволяет объединять несколько объявлений интерфейса с одинаковым именем в одно.

```ts

interface User {
  id: number;
  name: string;
}

interface User {
  email: string;
}

const user: User = {
  id: 1,
  name: 'John Doe',
  email: '<john.doe@example.com>'
};
```

- Типы не поддерживают объединение объявлений. Если попытаться определить два типа с одинаковыми именами, TypeScript выдаст ошибку.

```ts
type User = {
  id: number;
  name: string;
};

// Ошибка: Дублирующаяся идентификация 'User'
type User = {
  email: string;
};
```

## Использование в классах (Class Implementations)

Интерфейсы могут быть реализованы классами.

```ts

interface User {
  id: number;
  name: string;
}

class Person implements User {
  constructor(public id: number, public name: string) {}
}

const person = new Person(1, 'Jane Doe');
```

Типы не могут быть реализованы классами напрямую, но могут использоваться для создания типов свойств и методов класса.

```ts

type User = {
  id: number;
  name: string;
};

class Person {
  constructor(public user: User) {}
}

const person = new Person({ id: 1, name: 'Jane Doe' });

```

## Дженерики (Generics)

Дженерики позволяют создавать компоненты, которые работают с различными типами данных, обеспечивая типобезопасность. Они особенно полезны для создания обобщенных функций, классов и интерфейсов.
Пример использования дженериков:

```ts
// Обобщенная функция
function identity<T>(arg: T): T {
  return arg;
}

console.log(identity<number>(10)); // 10
console.log(identity<string>('Hello')); // Hello

// Обобщенный интерфейс
interface Box<T> {
  contents: T;
}

const numberBox: Box<number> = { contents: 42 };
const stringBox: Box<string> = { contents: 'Hello, World!' };

// Обобщенный класс
class DataHolder<T> {
  private data: T;

  constructor(initialData: T) {
    this.data = initialData;
  }

  getData(): T {
    return this.data;
  }

  setData(newData: T): void {
    this.data = newData;
  }
}

const numberHolder = new DataHolder<number>(100);
console.log(numberHolder.getData()); // 100
numberHolder.setData(200);
console.log(numberHolder.getData()); // 200

const stringHolder = new DataHolder<string>('Initial');
console.log(stringHolder.getData()); // Initial
stringHolder.setData('Updated');
console.log(stringHolder.getData()); // Updated
```

## Обобщенный пример

```ts
interface ApiResponse<T> {
  status: number;
  data: T;
}

type User = {
  id: number;
  name: string;
  email: string;
};

type Product = {
  id: number;
  name: string;
  price: number;
};

function fetchUser(): ApiResponse<User> {
  return {
    status: 200,
    data: {
      id: 1,
      name: 'Jane Doe',
      email: '<jane.doe@example.com>'
    }
  };
}

function fetchProduct(): ApiResponse<Product> {
  return {
    status: 200,
    data: {
      id: 101,
      name: 'Smartphone',
      price: 799
    }
  };
}

const userResponse = fetchUser();
console.log(userResponse.data.name); // Jane Doe

const productResponse = fetchProduct();
console.log(productResponse.data.name); // Smartphone
```
