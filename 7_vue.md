# vue 3

## Установка vue

[vite установка](https://vitejs.dev/guide/)

## Введение

Vue.js — это популярный фреймворк для создания реактивных пользовательских интерфейсов. В версии Vue 3 были введены новые возможности и улучшения, такие как script setup, которые делают разработку компонентов более простой и интуитивной. В этой лекции мы рассмотрим ключевые концепции Vue 3: v-model, script setup, emit, props, и ref.

Vue 3 предоставляет новый синтаксис для написания компонентов — `<script setup>`, который упрощает и улучшает разработку компонентов. В этой лекции мы рассмотрим, что такое `<script setup>`, его преимущества и как он используется для создания компонентов Vue 3.

### Что такое `<script setup>`

это упрощенный и оптимизированный способ написания логики компонента в Vue 3. Он объединяет декларацию реактивных данных, вычисляемых свойств, методов и других элементов компонента в одном месте, делая код более читабельным и эффективным.

### Преимущества `<script setup>`

Упрощенный синтаксис: Убирает необходимость использования export default и ключа setup.
Автоматический импорт реактивных функций: Функции, такие как ref, reactive, computed, автоматически доступны без необходимости их явного импорта.
Улучшенная производительность: Vue может оптимизировать компоненты, написанные с использованием `<script setut>`, благодаря статическому анализу кода.

1. Структура компонента с использованием `<script setup>`
Компонент Vue 3 с использованием `<script setup>` состоит из следующих основных частей:

- Шаблон (template)
- Логика (script setup)
- Стили (style)

### Пример базового компонента

```js
<template>
  <div>
    <p>{{ message }}</p>
    <button @click="updateMessage">Update Message</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Декларация реактивной переменной
const message = ref('Hello, Vue 3!');

// Метод для обновления сообщения
const updateMessage = () => {
  message.value = 'Message updated!';
};
</script>

<style scoped>
p {
  color: blue;
}
</style>
```

## Подробное объяснение частей компонента

### Шаблон (template)

Шаблон определяет разметку компонента. В нем используются директивы Vue, такие как v-bind и v-on, для привязки данных и обработки событий.
html

```js
<template>

  <div>
    <p>{{ message }}</p>
    <button @click="updateMessage">Update Message</button>
  </div>
</template>
```

В этом примере шаблон содержит:
Параграф, который отображает значение реактивной переменной message.
Кнопку, которая вызывает метод updateMessage при клике.

### Логика (script setup)

В секции`<script setup>` мы объявляем реактивные переменные, методы, вычисляемые свойства и другие элементы логики компонента.

```js
<script setup>
import { ref } from 'vue';

// Декларация реактивной переменной
const message = ref('Hello, Vue 3!');

// Метод для обновления сообщения
const updateMessage = () => {
  message.value = 'Message updated!';
};
</script>
```

В этом примере:
Мы импортируем функцию ref из Vue.
Объявляем реактивную переменную message с начальным значением 'Hello, Vue 3!'.
Объявляем метод updateMessage, который обновляет значение message.

### Стили (style)

Секция `<style>` используется для определения стилей компонента. Использование атрибута scoped ограничивает действие стилей только текущим файлом

## v-model

v-model — это директива Vue, которая используется для создания двустороннего связывания данных между моделью (данными) и представлением (шаблоном). Это полезно для создания интерактивных форм и элементов управления.
Пример использования v-model

```js
<template>
  <div>
    <input v-model="message" placeholder="Enter a message" />
    <p>{{ message }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const message = ref<string>('');
</script>
```

> В этом примере значение поля ввода связано с переменной message. Когда пользователь вводит текст, значение message автоматически обновляется, и наоборот.

## script setup

script setup — это новый способ объявления компонентов в Vue 3, который упрощает использование Composition API. Он позволяет писать логику компонента непосредственно внутри тега `<script>`, без необходимости явно определять функцию setup.
Пример компонента с использованием script setup

```ts
<template>
  <div>
    <h1>{{ message }}</h1>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const message = ref<string>('Hello, Vue 3 with script setup and TypeScript!');
</script>
```

## emit и props

### props — это способ передачи данных от родительского компонента к дочернему. emit используется для отправки событий из дочернего компонента обратно в родительский

Пример использования props и emit
Родительский компонент

```ts
<template>
  <div>
    <ChildComponent @customEvent="handleEvent" :parentMessage="message" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import ChildComponent from './ChildComponent.vue';

const message = ref<string>('Message from Parent');

const handleEvent = (payload: string) => {
  console.log('Event received:', payload);
};
</script>
</script>
```

Дочерний компонент

```ts
<template>
  <div>
    <p>{{ parentMessage }}</p>
    <button @click="emitEvent">Emit Event</button>
  </div>
</template>

<script setup lang="ts">
interface Props {
  parentMessage: string;
}

const props = defineProps<Props>();

const emit = defineEmits<{
  (e: 'customEvent', payload: string): void;
}>();

const emitEvent = () => {
  emit('customEvent', 'Payload from Child');
};
</script>
```

## ref

ref — это функция Vue, которая используется для создания реактивных переменных. Она позволяет отслеживать изменения данных и автоматически обновлять представление.
Пример использования ref

```ts
<template>

  <div>
    <button @click="increment">Increment</button>
    <p>Count: {{ count }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const count = ref(0);

const increment = () => {
  count.value++;
};
</script>
```

> В этом примере переменная count является реактивной. Когда значение count изменяется, это автоматически отражается в представлении.

## reactive

Функция reactive используется для создания реактивных объектов. Она возвращает проксированный объект, который отслеживает изменения своих свойств.
Пример использования reactive

```ts
<template>
  <div>
    <p>Name: {{ user.name }}</p>
    <p>Age: {{ user.age }}</p>
    <button @click="incrementAge">Increment Age</button>
  </div>
</template>

<script setup lang="ts">
import { reactive } from 'vue';

const user = reactive({
  name: 'John',
  age: 30,
});

const incrementAge = () => {
  user.age++;
};
</script>
```

В этом примере объект user является реактивным. Изменения в свойствах user автоматически отображаются в шаблоне.

## toRef, toRefs и defineModel

### toRef

Функция toRef используется для создания реактивной ссылки на одно свойство объекта. Это полезно, когда нужно передать отдельное свойство объекта как реактивную ссылку.
Пример использования toRef

```ts
<template>

  <div>
    <input v-model="nameRef" placeholder="Enter your name" />
    <p>{{ nameRef }}</p>
  </div>
</template>

<script setup lang="ts">
import { reactive, toRef } from 'vue';

const user = reactive({
  name: 'John Doe',
  age: 30,
});

const nameRef = toRef(user, 'name');
</script>
```

В этом примере мы создаем реактивную ссылку nameRef на свойство name объекта user. При изменении значения nameRef также изменяется значение user.name.

### toRefs

Функция toRefs используется для преобразования всех свойств реактивного объекта в реактивные ссылки. Это полезно, когда нужно передать весь объект как отдельные реактивные ссылки.
Пример использования toRefs

```ts
<template>
  <div>
    <input v-model="name" placeholder="Enter your name" />
    <input v-model="age" placeholder="Enter your age" type="number" />
    <p>Name: {{ name }}</p>
    <p>Age: {{ age }}</p>
  </div>
</template>

<script setup lang="ts">
import { reactive, toRefs } from 'vue';

const user = reactive({
  name: 'John Doe',
  age: 30,
});

const { name, age } = toRefs(user);
</script>
```

В этом примере мы преобразуем объект user в отдельные реактивные ссылки name и age с помощью функции toRefs. Теперь мы можем использовать эти ссылки отдельно в шаблоне.

### deifneModel

Родительский компонент

```ts
<template>
  <div>
    <ChildComponent v-model="message" />
    <p>Parent Message: {{ message }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import ChildComponent from './ChildComponent.vue';

const message = ref<string>('Hello from Parent');
</script>
```

Дочерний компонент

```ts
<template>
  <div>
    <input v-model="localMessage" placeholder="Enter a message" />
    <p>Child Message: {{ localMessage }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue';

const model = defineModel<string>('modelValue');
const localMessage = ref<string>(model.value);

// Слежение за изменениями локальной переменной и обновление модели
watch(localMessage, (newValue) => {
  model.value = newValue;
});

// Слежение за изменениями модели и обновление локальной переменной
watch(model, (newValue) => {
  localMessage.value = newValue;
});
</script>
```

Родительский компонент содержит переменную message, которая передается дочернему компоненту с использованием директивы v-model.
Дочерний компонент:
В дочернем компоненте мы используем функцию defineModel для определения модели. В данном случае, defineModel принимает строку 'modelValue', что соответствует директиве v-model в родительском компоненте.
Мы создаем локальную реактивную переменную localMessage и инициализируем ее значением модели model.value.
Два watch выражения используются для синхронизации изменений между локальной переменной localMessage и моделью:
Первый watch следит за изменениями localMessage и обновляет значение модели model.value.
Второй watch следит за изменениями модели и обновляет значение локальной переменной localMessage.
Таким образом, изменения, внесенные в поле ввода в дочернем компоненте, будут автоматически отображаться в родительском компоненте и наоборот.

## Пример использования toRefs и toRef для props

Родительский компонент
В родительском компоненте мы передадим объект user в дочерний компонент в качестве props.

```ts
<template>
  <div>
    <UserCard :user="user" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import UserCard from './UserCard.vue';

interface User {
  name: string;
  age: number;
  email: string;
}

const user = ref<User>({
  name: 'John Doe',
  age: 30,
  email: 'john.doe@example.com'
});
</script>
```

Дочерний компонент с использованием toRefs
В дочернем компоненте мы можем использовать toRefs для преобразования всех свойств объекта props в реактивные ссылки.

```ts
<template>
  <div>
    <p>Name: {{ name }}</p>
    <p>Age: {{ age }}</p>
    <p>Email: {{ email }}</p>
  </div>
</template>

<script setup lang="ts">
import { toRefs } from 'vue';

interface User {
  name: string;
  age: number;
  email: string;
}

const props = defineProps<{ user: User }>();

const { name, age, email } = toRefs(props.user);
</script>
```

В этом примере мы используем toRefs для преобразования всех свойств объекта user в отдельные реактивные ссылки name, age и email.
Дочерний компонент с использованием toRef
Если нам нужно работать только с одним свойством объекта props, можно использовать toRef для создания реактивной ссылки на это свойство.

```ts
<template>
  <div>
    <p>Name: {{ name }}</p>
  </div>
</template>

<script setup lang="ts">
import { toRef } from 'vue';

interface User {
  name: string;
  age: number;
  email: string;
}

const props = defineProps<{ user: User }>();

const name = toRef(props.user, 'name');
</script>
```

В этом примере мы используем toRef для создания реактивной ссылки name на свойство name объекта user.
Объяснение
Родительский компонент:
Мы определяем интерфейс User, который описывает структуру объекта user.
Переменная user создается с использованием типа User и передается в дочерний компонент UserCard через props.

Дочерний компонент с использованием toRefs:
Мы определяем интерфейс User, который описывает структуру объекта user.
Функция `defineProps` используется для определения типа props в компоненте.
Функция toRefs преобразует все свойства объекта props.user в отдельные реактивные ссылки. Это позволяет нам работать с этими свойствами как с отдельными реактивными переменными.
Дочерний компонент с использованием toRef:
Мы определяем интерфейс User, который описывает структуру объекта user.
Функция toRef создаёт реактивную ссылку на одно конкретное свойство объекта props.user. Это полезно, когда нужно работать только с одним свойством объекта.

## computed

Функция computed используется для создания вычисляемых свойств. Вычисляемые свойства автоматически обновляются при изменении зависимостей.
Пример использования computed

```ts
<template>
  <div>
    <p>Full Name: {{ fullName }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';

const firstName = ref<string>('John');
const lastName = ref<string>('Doe');

const fullName = computed(() => `${firstName.value} ${lastName.value}`);
</script>
```
