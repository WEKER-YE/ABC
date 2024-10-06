VUEX
1. 確認 Vuex store 已在全局註冊
首先，確保你的 store/index.js 文件中的 Vuex store 已經在應用中全局註冊。這通常是在 main.ts（或 main.js）中進行的：

ts
複製程式碼
// main.ts (或 main.js)
import { createApp } from 'vue';
import App from './App.vue';
import store from './store';  // 引入 Vuex store

createApp(App)
  .use(store)  // 全局註冊 Vuex store
  .mount('#app');

2. 在 Vue 組件中正確使用 Vuex Store(此為現代嚴謹寫法)
你可以使用 this.$store（傳統方法）來訪問 Vuex 的 state，但在 Vue 3 的 TypeScript 中，更推薦使用 setup() 並搭配 useStore() 函數來訪問 store。這樣可以確保 TypeScript 的類型推斷更加準確。

這是使用 Vuex Store 的範例代碼：

```HTML
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
重要點：
useStore()：在 Vue 3 中，可以使用 useStore() 來訪問 Vuex store。這是 Vuex 4 的一個新方法，適用於 Vue 3 中的組件。
TypeScript 支援：如果你希望為 Vuex store 添加 TypeScript 支援，確保你在 store/index.js 或 store/index.ts 中為 state 定義了相應的類型。

3傳統寫法
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

傳統寫法在在其他版本上會遇到一些模組上問題

可以現檢查store部分
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

再 為 Vue 組件的 this.$store 提供類型支援
接下來，你需要在 Vue 組件中為 this.$store 提供類型支持。你可以使用 ComponentCustomProperties 來擴展 Vue 組件中的 this，讓 TypeScript 能夠識別 this.$store 的類型。

在 src 文件夾中創建一個 vuex.d.ts 文件來擴展 Vue 的 this 屬性。
// vuex.d.ts
import { Store } from 'vuex';
import { State } from './store';  // 引入你定義的 state 類型

declare module '@vue/runtime-core' {
  // 為 `this.$store` 提供類型宣告
  interface ComponentCustomProperties {
    $store: Store<State>;
  }
}
