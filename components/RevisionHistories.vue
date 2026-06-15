<script setup lang="ts">
import { ref } from "vue";

interface Revision {
  date: string;
  content: string;
}

defineProps<{
  revisions: Revision[];
}>();

const isOpen = ref(false);
</script>

<template>
  <div class="revision-history">
    <button class="trigger" @click="isOpen = !isOpen">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round"
      >
        <path d="M12 8v4l3 3" />
        <circle cx="12" cy="12" r="10" />
      </svg>
      <span class="text-xs">改訂履歴</span>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="12"
        height="12"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round"
        class="chevron"
        :class="{ open: isOpen }"
      >
        <polyline points="6 9 12 15 18 9" />
      </svg>
    </button>
    <Transition name="expand">
      <ul v-if="isOpen" class="list">
        <li v-for="rev in revisions" :key="rev.date" class="item">
          <span class="date">{{ rev.date }}</span>
          <span class="content">{{ rev.content }}</span>
        </li>
      </ul>
    </Transition>
  </div>
</template>

<style scoped>
.revision-history {
  position: absolute;
  top: 3em;
  right: 0.5em;
  font-size: 0.36em;
  z-index: 100;
  display: flex;
  flex-direction: column;
}

.trigger {
  display: flex;
  align-items: center;
  gap: 4px;
  cursor: pointer;
  background: none;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 8px;
  color: #666;
  font-size: 1em;
  transition: background 0.2s;
  align-self: flex-end;
}

.trigger:hover {
  background: #f0f0f0;
}

.chevron {
  transition: transform 0.2s;
}

.chevron.open {
  transform: rotate(180deg);
}

.list {
  list-style: none;
  padding: 0.5em 1em;
  margin: 0.25em 0 0;
  background: #fafafa;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

ul.list > li::before {
  display: none;
}

.item {
  display: flex;
  gap: 1em;
  padding: 4px 0;
  align-items: baseline;
}

.item + .item {
  border-top: 1px solid #eee;
}

.date {
  color: #888;
  white-space: nowrap;
  font-family: monospace;
}

.content {
  color: #333;
}

.expand-enter-active,
.expand-leave-active {
  transition:
    opacity 0.2s,
    transform 0.2s;
}

.expand-enter-from,
.expand-leave-to {
  opacity: 0;
  transform: translateY(-4px);
}
</style>
