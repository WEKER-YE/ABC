
# Vuex 與 TypeScript 使用指南

## 1. 全局註冊 Vuex Store

首先，確保你的 `store/index.js` 或 `store/index.ts` 文件中的 Vuex store 已經在應用中全局註冊。這通常是在 `main.ts`（或 `main.js`）中進行的：

```ts
// main.ts (或 main.js)
import { createApp } from 'vue';
import App from './App.vue';
import store from './store';  // 引入 Vuex store

createApp(App)
  .use(store)  // 全局註冊 Vuex store
  .mount('#app');
```

## 2. 在 Vue 組件中正確使用 Vuex Store

### 使用 `setup()` 與 `useStore()` 的現代寫法

在 Vue 3 和 TypeScript 中，推薦使用 `setup()` 和 `useStore()` 函數來訪問 Vuex store。這樣可以確保 TypeScript 正確推斷 `store` 的類型。

```vue
<template>
  <div class="home">
    <h1>{{ greeting }}</h1>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { useStore } from 'vuex';

export default defineComponent({
  name: 'HomeView',
  setup() {
    const store = useStore();  // 使用 useStore 函數獲取 Vuex Store 實例
    const greeting = store.state.greeting;  // 從 Vuex state 中獲取 greeting

    return {
      greeting
    };
  }
});
</script>
```

### 重點說明：
- **`useStore()`**：在 Vue 3 中，`useStore()` 函數可以用來訪問 Vuex store。這是 Vuex 4 的一個新方法，適合 Vue 3 的 `setup()` 函數。
- **TypeScript 支援**：如果你希望為 Vuex store 添加 TypeScript 支援，確保你在 `store/index.ts` 中為 `state` 定義了相應的類型。

### `store/index.ts` 的範例

```ts
// store/index.ts
import { createStore } from 'vuex';

// 定義 state 的類型
interface State {
  greeting: string;
}

// 創建 Vuex store 並定義 state
const store = createStore<State>({
  state: {
    greeting: 'Hello from Vuex!'
  },
  mutations: {},
  actions: {},
  modules: {}
});

export default store;
```

## 3. 傳統寫法：使用 `computed` 方式

你仍然可以使用傳統的 `computed` 屬性來訪問 Vuex store，這種方式更接近 Vue 2 的用法：

```vue
<template>
  <div class="home">
    <h1>{{ greeting }}</h1>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'HomeView',
  computed: {
    greeting() {
      return this.$store.state.greeting;  // 從 Vuex 中提取 greeting
    }
  }
});
</script>
```

## 4. 為 Vue 組件的 `this.$store` 提供類型支援

為了讓 TypeScript 正確識別 `this.$store`，我們需要擴展 Vue 組件中的 `this` 屬性。你可以在 `src` 文件夾中創建一個 `vuex.d.ts` 文件來擴展 Vue 的 `this` 屬性。

### `vuex.d.ts` 文件範例

```ts
// vuex.d.ts
import { Store } from 'vuex';
import { State } from './store';  // 引入你定義的 state 類型

declare module '@vue/runtime-core' {
  // 為 `this.$store` 提供類型宣告
  interface ComponentCustomProperties {
    $store: Store<State>;
  }
}
```
