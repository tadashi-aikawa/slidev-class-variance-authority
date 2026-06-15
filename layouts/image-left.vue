<script setup lang="ts">
import { computed } from "vue";

const props = withDefaults(
  defineProps<{
    image?: string;
    backgroundSize?: string;
    backgroundPosition?: string;
    ratio?: string;
  }>(),
  {
    backgroundSize: "cover",
    backgroundPosition: "center",
    ratio: "50%",
  },
);

const resolveAssetUrl = (url: string): string => {
  if (url.startsWith("/")) {
    return `${import.meta.env.BASE_URL}${url.slice(1)}`;
  }
  return url;
};

const imageStyle = computed(() => ({
  backgroundImage: props.image
    ? `url("${resolveAssetUrl(props.image)}")`
    : undefined,
  backgroundRepeat: "no-repeat",
  backgroundPosition: props.backgroundPosition,
  backgroundSize: props.backgroundSize,
}));

const gridStyle = computed(() => ({
  display: "grid",
  gridTemplateColumns: `${props.ratio} 1fr`,
}));
</script>

<template>
  <div
    class="slidev-layout h-full w-full gap-[1.5em] !py-0 !pl-0"
    :style="gridStyle"
  >
    <div class="h-full" :style="imageStyle" />
    <div class="py-[1em] pr-[2em]">
      <slot />
    </div>
  </div>
</template>
