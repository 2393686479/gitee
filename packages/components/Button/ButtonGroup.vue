<template>
  <div class="er-button-group"></div>
</template>

<script lang="ts" setup>
import type { ButtonGroupProps } from "./types";
import { BUTTON_GROUP_CTX_KEY } from "./contants";
import { provide, reactive, toRef } from "vue";

defineOptions({
  name: "ErButtonGroup",
});

const props = defineProps<ButtonGroupProps>();

provide(
  BUTTON_GROUP_CTX_KEY,
  reactive({
    size: toRef(props, "size"),
    type: toRef(props, "type"),
    disabled: toRef(props, "disabled"),
  })
);
</script>

<style scoped>
@import "./style.css";
</style>
