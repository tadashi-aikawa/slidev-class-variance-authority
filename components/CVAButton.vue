<script setup lang="ts">
import { cva, type VariantProps } from "class-variance-authority";

const buttonVariants = cva(
  "inline-flex items-center rounded font-medium", // 共通項目
  {
    variants: {
      // variantの属性値により付与するクラスを定義
      variant: {
        primary: "bg-blue-600 text-white hover:bg-blue-700",
        danger: "bg-red-600 text-white hover:bg-red-700",
        outline:
          "border border-gray-300 bg-white text-gray-900 hover:bg-gray-50",
      },
      // sizeの属性値により付与するクラスを定義
      size: {
        sm: "min-h-8 px-3 py-1 text-sm",
        md: "min-h-10 px-4 py-2 text-base",
        lg: "min-h-12 px-6 py-3 text-lg",
      },
      // disabledの属性値により付与するクラスを定義
      disabled: {
        true: "disabled:pointer-events-none disabled:opacity-50",
        false: null,
      },
    },
    // 属性値が未指定の場合に付与するクラス定義(default値)
    defaultVariants: {
      variant: "primary",
      size: "md",
      disabled: false,
    },
  },
);

// buttonVariantsから型を定義
type ButtonVariants = VariantProps<typeof buttonVariants>;

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
