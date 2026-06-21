<script setup lang="ts">
withDefaults(
  defineProps<{
    variant?: "primary" | "danger" | "outline";
    size?: "sm" | "md" | "lg";
    disabled?: boolean;
  }>(),
  {
    variant: "primary",
    size: "md",
    disabled: false,
  },
);
</script>

<template>
  <button
    :disabled="disabled"
    class="inline-flex items-center rounded font-medium"
    :class="[
      {
        'bg-blue-600 text-white hover:bg-blue-700': variant === 'primary',
        'bg-red-600 text-white hover:bg-red-700': variant === 'danger',
        'border border-gray-300 bg-white text-gray-900 hover:bg-gray-50':
          variant === 'outline',

        'min-h-8 px-3 py-1 text-sm': size === 'sm',
        'min-h-10 px-4 py-2 text-base': size === 'md',
        'min-h-12 px-6 py-3 text-lg': size === 'lg',

        'disabled:pointer-events-none disabled:opacity-50': disabled,
      },
    ]"
  >
    <slot />
  </button>
</template>
