# Pinia

Pinia — это современная библиотека для управления состоянием в приложениях на Vue 3. Она предоставляет мощный и простой API и является официальным решением для управления состоянием в Vue 3. В этой лекции мы рассмотрим, как подключить и использовать Pinia с TypeScript в ваших проектах Vue 3.
[pinia](https://pinia.vuejs.org/getting-started.html)

## Установка Pinia

Для начала необходимо установить Pinia в ваш проект. Это можно сделать с помощью npm или yarn.
bash
Copy

- С использованием npm
    npm install pinia

- С использованием yarn
    yarn add pinia

## Подключение Pinia к проекту Vue 3

После установки Pinia необходимо подключить его к вашему проекту. Это делается в основном файле вашего проекта, обычно в main.ts.
typescript
main.ts

```ts
import { createApp } from 'vue';
import { createPinia } from 'pinia';
import App from './App.vue';

const app = createApp(App);

// Создаем экземпляр Pinia и подключаем его к приложению
const pinia = createPinia();
app.use(pinia);

app.mount('#app');
```

## Создание Store с использованием Pinia и Composition API

> Создадим новый файл stores/counter.ts для нашего store.

```ts
// stores/counter.ts
import { defineStore } from 'pinia';
import { ref, computed } from 'vue';

// Определяем интерфейс для состояния
interface CounterState {
  count: number;
}

// Создаем store
export const useCounterStore = defineStore('counter', () => {
  // Создаем реактивное состояние
  const count = ref(0);

  // Создаем вычисляемое свойство
  const doubleCount = computed(() => count.value * 2);

  // Создаем действие
  const increment = () => {
    count.value++;
  };

  return {
    count,
    doubleCount,
    increment,
  };
});
```

В этом примере мы:
Используем defineStore с функцией для создания store.
Используем Composition API для определения реактивных данных (ref), вычисляемых свойств (computed) и действий.

## Использование Store в Компонентах

Теперь давайте используем наш store в компоненте Vue.

```ts
<template>
  <div>
    <p>Count: {{ count }}</p>
    <p>Double Count: {{ doubleCount }}</p>
    <button @click="increment">Increment</button>
  </div>
</template>

<script setup lang="ts">
import { useCounterStore } from '@/stores/counter';

const counterStore = useCounterStore();

const { count, doubleCount, increment } = counterStore;
</script>
```

В этом компоненте мы:
Импортируем и используем наш store useCounterStore.
Деструктурируем и используем count, doubleCount и increment внутри компонента.
