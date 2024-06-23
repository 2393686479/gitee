<script setup>
import { onMounted, reactive, ref } from "vue";
const b = ref();
// onMounted(() => {
//   console.log(b.value);
//   console.log(b.value?.ref);
// });

const args = reactive(({
  accordion: true,
  modelValue: ["a"]
}))

console.log(args.accordion)
</script>

<template>
  <er-button size="small" ref="b">www</er-button>

  <er-collapse v-bind="args">
    <er-collapse-item name="a" title="Title a">
      <div>this is content a</div>
    </er-collapse-item>
    <er-collapse-item name="b" title="title b">
      <div>this is content b</div>
    </er-collapse-item>
    <er-collapse-item name="c" title="title c  disable" disabled>
      <div>this is content c</div>
    </er-collapse-item>
  </er-collapse>

  
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
