<script setup lang="ts">
import { ref } from 'vue'

interface Props {
  items: {
    title: string
    key: string
  }[]
}
const props = defineProps<Props>()

const isActiveKey = ref<string>('')

const toggleActive = (key: string) => {
  if (isActiveKey.value === key) {
    isActiveKey.value = ''
  } else {
    isActiveKey.value = key
  }
}

const start = (element: any) => {
  element.style.height = element.scrollHeight + 'px'
}

const end = (element: any) => {
  element.style.height = ''
}
</script>

<template>
  <div
    v-for="{ title, key } in items"
    class="accordion"
    :class="{ 'accordion--active': isActiveKey === key }"
    role="button"
    @click="() => toggleActive(key)"
  >
    <!-- HEADER -->
    <div class="accordion__header">
      <slot name="header" :toggleActive>
        <h4>{{ title }}</h4>
        <button class="accordion__button">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            width="24"
            height="24"
            color="#000000"
            fill="none"
          >
            <path
              d="M9.00005 6C9.00005 6 15 10.4189 15 12C15 13.5812 9 18 9 18"
              stroke="currentColor"
              stroke-width="1.5"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
        </button>
      </slot>
    </div>
    <!-- BODY SLOT -->
    <transition
      name="accordion"
      @enter="start"
      @after-enter="end"
      @before-leave="start"
      @after-leave="end"
    >
      <div v-if="isActiveKey === key" class="accordion__body">
        <slot v-if="$slots[key]" :name="key" />
      </div>
    </transition>
  </div>
</template>

<style scoped>
.accordion--active .accordion__button {
  transform: rotate(90deg);
}

.accordion__header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 0;
  background: #f5f5f5;
}

.accordion__button {
  transition: all 0.2s linear;
}

.accordion-enter-active,
.accordion-leave-active {
  will-change: height, opacity;
  transition:
    height 0.3s ease,
    opacity 0.3s ease;
  overflow: hidden;
}

.accordion-enter-from,
.accordion-leave-to {
  height: 0 !important;
  opacity: 0;
}
</style>
