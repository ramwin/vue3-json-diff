<template>
  <div class="vue3-json-diff">
    <div class="item">
      <json-viewer :value="props.leftValue" />
    </div>
    <div class="item diff">
      <div v-html="diffHtml"></div>
    </div>
    <div class="item">
      <json-viewer :value="props.rightValue" />
    </div>
  </div>
</template>
<script setup lang="ts">
import { computed } from "vue"
import { JsonViewer } from "vue3-json-viewer"
import { diff_match_patch, diff_prettyHtml } from "diff-match-patch"
import "vue3-json-viewer/dist/index.css";

const props = defineProps({
  leftValue: {
    type: null,
    required: true,
  },
  rightValue: {
    type: null,
    required: true,
  }
})

const diffHtml = computed(()=>{
  const obj = new diff_match_patch()
  const left_string = JSON.stringify(props.leftValue, null, 4)
  const right_string = JSON.stringify(props.rightValue, null, 4)
  console.log("计算区别", left_string, right_string)
  const diff = obj.diff_main(
    left_string, right_string
  )
  console.log("区别: ", diff)
  const html = obj.diff_prettyHtml(
    diff
  )
  return html
})
</script>
<style scoped lang="less">
.vue3-json-diff {
  width: 100%;
  padding: 0.3rem;
  box-sizing: border-box;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  .item {
    width: 33%;
    min-width: 300px;
    border: 1px solid #ccc;
    &.diff {
      padding: 0.8rem;
    }
  }
}
</style>
