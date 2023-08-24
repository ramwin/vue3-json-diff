<template>
  <div class="vue3-json-diff">
    <JsonViewer :value="left_data" />
    <div>
      <div v-html="diff_data"></div>
    </div>
    <JsonViewer :value="right_data" />
  </div>
</template>
<script setup lang="ts">
import JsonViewer from "vue-json-viewer"
import { computed } from "vue"
// import { diffString, diff } from "json-diff"
import DiffMatchPatch from "diff-match-patch"

const props = defineProps({
  "left_data": {
    type: Object,
    required:true,
  },
  "right_data": {
    type: Object,
    required:true,
  },
})

console.info("user Vue3JsonDiff")
const diff_data = computed((): String=>{
  // return diffString(props.left_data, props.right_data, {color: false})
  // diff('123', '455', {color: false})
  // const result = '123';
  // diff_match_patch.diff_main()
  const dmp = new DiffMatchPatch();
  const diff_array = dmp.diff_main(
    JSON.stringify(props.left_data),
    JSON.stringify(props.right_data))
  const diff = dmp.diff_prettyHtml(diff_array);
  
  console.log("difference: ", diff)
  return diff
})
</script>

<style>
.vue3-json-diff {
  display: flex;
  justify-content: space-between;
}
</style>
