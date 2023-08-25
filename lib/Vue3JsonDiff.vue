<template>
  <div class="vue3-json-diff">
    <div class="item">
      <json-viewer :value="props.leftValue" />
    </div>
    <div class="item">
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
  const left_string = JSON.stringify(props.leftValue)
  const right_string = JSON.stringify(props.rightValue)
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
  display: flex;
  .item {
    width: 30%;
  }
}
</style>
