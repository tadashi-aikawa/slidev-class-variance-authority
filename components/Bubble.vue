<script setup lang="ts">
defineProps<{
  image: string;
  imageWidth?: string;
  imageHeight?: string;
  imageGap?: string;
  name?: string;
  direction: "left" | "right" | "top";
}>();
</script>

<template>
  <div
    class="character-bubble"
    :class="direction"
    :style="{ gap: imageGap ?? '1.2rem' }"
  >
    <img
      class="character"
      :src="image"
      :style="{
        width: imageWidth ? `${imageWidth}px` : 'auto',
        height: imageHeight ? `${imageHeight}px` : 'auto',
      }"
    />

    <div class="bubble">
      <div v-if="name" class="name">{{ name }}</div>
      <div class="text">
        <slot />
      </div>
    </div>
  </div>
</template>

<style scoped>
.character-bubble {
  display: flex;
  align-items: flex-start;
  margin: 2rem 0;
}

.character-bubble.left {
  flex-direction: row-reverse;
}

.character-bubble.right {
  flex-direction: row;
}

.character-bubble.top {
  flex-direction: column-reverse;
  align-items: center;
}

.character {
  object-fit: contain;
}

.bubble {
  position: relative;
  max-width: 800px;
  padding: 1rem 1.4rem;
  border-radius: 1.2rem;
  background: white;
  box-shadow: 0 4px 24px rgb(0 0 0 / 18%);
  font-size: 2rem;
  line-height: 1.6;
}

.bubble::before {
  content: "";
  position: absolute;
  top: 28px;
  width: 0;
  height: 0;
  border: 14px solid transparent;
}

.left .bubble::before {
  right: -26px;
  border-left-color: white;
}

.right .bubble::before {
  left: -26px;
  border-right-color: white;
}

.top .bubble::before {
  bottom: -26px;
  left: 50%;
  top: auto;
  transform: translateX(-50%);
  border-top-color: white;
}

.name {
  margin-bottom: 0.25rem;
  font-weight: 700;
  font-size: 1.3rem;
}
</style>
