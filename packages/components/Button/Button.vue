<template>
  <component
    :is="tag"
    ref="_ref"
    class="er-button"
    :autofocus="autofocus"
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
    @click="
      (e: MouseEvent) =>
        useThrottle ? handleBtnClickThrottle(e) : handleBtnClick(e)
    "
  >
    <template v-if="loading">
      <slot name="loading">
        <er-icon
          class="loading-icon"
          :icon="loadingIcon ?? 'spinner'"
          :style="iconStyle"
          spin
        />
      </slot>
    </template>
    <er-icon
      v-if="icon && !loading"
      :icon="icon"
      :style="iconStyle"
      size="1x"
    />
    <slot></slot>
  </component>
</template>

<script setup lang="ts">
import { ref, computed, inject } from "vue";
import type { ButtonProps, ButtonEmits, ButtonInstance } from "./types";
import { throttle } from "lodash-es";
import ErIcon from "../Icon/Icon.vue";
import { BUTTON_GROUP_CTX_KEY } from "./contants";

defineOptions({ name: "ErButton" });

const props = withDefaults(defineProps<ButtonProps>(), {
  tag: "button",
  nativeType: "button",
  useThrottle: true,
  throttleDuration: 500,
});

const ctx = inject(BUTTON_GROUP_CTX_KEY, void 0);

const size = computed(() => ctx?.size ?? props?.size ?? "");

const type = computed(() => ctx?.type ?? props?.type ?? "");

const disabled = computed(() => ctx?.disabled || props.disabled || false);

const slots = defineSlots();

const _ref = ref<HTMLButtonElement>();

const emits = defineEmits<ButtonEmits>();

const handleBtnClick = (e: MouseEvent) => emits("click", e);

const handleBtnClickThrottle = throttle(handleBtnClick, props.throttleDuration);

const iconStyle = computed(() => ({
  marginRight: slots.default ? "6px" : "0px",
}));
defineExpose<ButtonInstance>({
  ref: _ref,
});
</script>

<style scoped>
@import "./style.css";
</style>
