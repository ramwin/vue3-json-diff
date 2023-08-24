<script setup lang="ts">
  import {ref} from "vue"
  import Vue3JsonDiff from "../components/Vue3JsonDiff.vue"
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
        :left_data="left_data"
        :right_data="right_data"
    />
  </main>
</template>
