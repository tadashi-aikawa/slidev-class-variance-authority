<script setup lang="ts">
type ButtonVariant = "primary" | "danger" | "outline";
type ButtonSize = "sm" | "md" | "lg";

const props = withDefaults(
  defineProps<{
    variant?: ButtonVariant;
    size?: ButtonSize;
    disabled?: boolean;
  }>(),
  {
    variant: "primary",
    size: "md",
    disabled: false,
  },
);

const variantClasses: Record<ButtonVariant, string> = {
  primary: "bg-blue-600 text-white hover:bg-blue-700",
  danger: "bg-red-600 text-white hover:bg-red-700",
  outline: "border border-gray-300 bg-white text-gray-900 hover:bg-gray-50",
};

const sizeClasses: Record<ButtonSize, string> = {
  sm: "min-h-8 px-3 py-1 text-sm",
  md: "min-h-10 px-4 py-2 text-base",
  lg: "min-h-12 px-6 py-3 text-lg",
};
</script>

<template>
  <button
    :disabled="disabled"
    class="inline-flex items-center rounded font-medium"
    :class="[
      variantClasses[props.variant],
      sizeClasses[props.size],
      {
        'disabled:pointer-events-none disabled:opacity-50': props.disabled,
      },
    ]"
  >
    <slot />
  </button>
</template>
