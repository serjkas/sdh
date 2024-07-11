# TS

### Аргументы

Аргументы представляют собой значения, передаваемые в функцию при ее вызове. В TypeScript мы можем указывать типы для аргументов функций, чтобы обеспечить более явное и безопасное использование.

```typescript
function greet(name: string) {
console.log("Hello, " + name + "!");
}

greet("John"); // Выведет "Hello, John!"
greet(123); // Ошибка компиляции: аргумент должен быть строкой
```

### Типы и интерфейсы

TypeScript предоставляет мощные возможности для создания пользовательских типов с помощью интерфейсов. Интерфейсы определяют, какие свойства или методы должны присутствовать у объектов или классов.

```typescript
interface Person {
name: string;
age: number;
}

function displayPersonInfo(person: Person) {
console.log("Name: " + person.name);
console.log("Age: " + person.age);
}

let john: Person = {
name: "John",
age: 25
};

displayPersonInfo(john); // Выведет информацию о John
```

### Record

Record - это удобный тип данных, позволяющий создавать объекты с динамическими ключами и значениями.

```typescript
const fruits: Record = {
apple: "red",
banana: "yellow",
orange: "orange"
};

console.log(fruits.apple); // Выведет "red"
console.log(fruits.grape); // Ошибка компиляции: ключ не существует
```

### Axios

Axios - это библиотека для выполнения HTTP-запросов в JavaScript и TypeScript. Она предоставляет удобные методы для работы с API, обладает синтаксисом, приятным для использования.

```typescript
import axios from "axios";

async function fetchData() {
try {
const response = await axios.get("Открыть");
console.log(response.data);
} catch (error) {
console.error(error);
}
}

fetchData();
```

## Дополнительные темы

### Классы и наследование

Классы - это основа объектно-ориентированного программирования в TypeScript. Они позволяют создавать объекты с определенными свойствами и методами. Наследование позволяет создавать классы, которые наследуют свойства и методы от других классов.

```typescript
class Animal {
protected name: string;

constructor(name: string) {
this.name = name;
}

makeSound() {
console.log("The animal makes a sound.");
}
}

class Dog extends Animal {
makeSound() {
console.log("The dog barks.");
}
}

const dog = new Dog("Buddy");
console.log(dog.name); // "Buddy"
dog.makeSound(); // "The dog barks."
```

### Модули и экспорт/импорт

Модули позволяют организовать код в удобные для повторного использования блоки. В TypeScript вы можете экспортировать и импортировать значения из модулей.

```typescript
// file1.ts
export const PI = 3.14;
export function square(x: number) {
return x * x;
}

// file2.ts
import { PI, square } from "./file1";

console.log(PI); // 3.14
console.log(square(2)); // 4
```

### Дженерики

Дженерики позволяют создавать обобщенный код, который может работать с разными типами данных. Они позволяют параметризовать типы и повышают гибкость и безопасность кода.

```typescript
function identity(value: T): T {
return value;
}

const result = identity("Hello");
console.log(result); // "Hello"
```

### Декораторы

Декораторы предоставляют синтаксический сахар для изменения классов и их членов во время выполнения или на этапе компиляции. Они широко используются во фреймворках и библиотеках для добавления дополнительного функционала к классам и методам.

```typescript
function log(target: any, key: string, descriptor: PropertyDescriptor) {
const originalMethod = descriptor.value;

descriptor.value = function(...args: any[]) {
console.log(`Calling ${key} with arguments: ${args}`);
return originalMethod.apply(this, args);
};

return descriptor;
}

class Calculator {
@log
add(a: number, b: number) {
return a + b;
}
}

const calculator = new Calculator();
console.log(calculator.add(2, 3)); // Calling add with arguments: 2, 3 // 5
```
