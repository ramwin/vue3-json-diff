# Vue 3 + TypeScript + Vite

# Install
```
npm install --save vue3-json-diff
```

# Usage
```html
<script setup lang="ts">
  import {ref} from "vue"
  import Vue3JsonDiff from "vue3-json-diff"
  import "vue3-json-diff/dist/style.css"
  const left_data = ref({
    id: 18,
    name: "alice",
  })
  const right_data = ref({
    id: 18,
    name: "bob",
  })
</script>

<template>
  <main>
    <Vue3JsonDiff
        :left-value="left_data"
        :right-value="right_data"
    />
  </main>
</template>
```
