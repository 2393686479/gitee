<template>
  <component
    :is="tag"
    ref="_ref"
    class="er-button"
    :type="tag === 'button' ? nativeType : void 0"
    :disabled="disabled || loading ? true : false"
    :class="{
      [`er-button--${type}`]: type,
      [`er-button--${size}`]: size,
      'is-plain': plain,
      'is-round': round,
      'is-circle': circle,
      'is-disabled': disabled,
      'is-loading': loading,
    }"
  >
    <slot></slot>
  </component>
</template>

<script setup lang="ts">
import { ref } from "vue";
import type { ButtonProps, ButtonEmits, ButtonInstance } from "./types";
import { throttle } from "lodash-es";
defineOptions({ name: "ErButton" });

const props = withDefaults(defineProps<ButtonProps>(), {
  tag: "button",
  nativeType: "button",
});

const slots = defineSlots();

const _ref = ref<HTMLButtonElement>();

const emits = defineEmits<ButtonEmits>();

defineExpose<ButtonInstance>({
  ref: _ref,
});
</script>

<style scoped>
@import "./style.css";
</style>
