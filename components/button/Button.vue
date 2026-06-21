<script setup lang="ts">
import { buttonVariants, ButtonVariants } from ".";

defineProps<{
  variant?: ButtonVariants["variant"];
  size?: ButtonVariants["size"];
  disabled?: ButtonVariants["disabled"];
}>();
</script>

<template>
  <button
    :class="buttonVariants({ variant, size, disabled })"
    :disabled="!!disabled"
  >
    <slot />
  </button>
</template>
