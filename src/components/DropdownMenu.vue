<template>
  <div class="relative inline-block w-56" ref="menuRef">
    <button
      @click="toggle"
      class="w-full flex justify-between items-center px-4 py-2 bg-blue-400 hover:bg-blue-500 text-white font-medium rounded shadow"
    >
      <span>{{ selected?.label || 'Select an option' }}</span>
      <svg
        class="w-4 h-4 ml-2 transition-transform"
        :class="{ 'rotate-180': open }"
        fill="none" stroke="currentColor" viewBox="0 0 24 24"
      >
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
          d="M19 9l-7 7-7-7" />
      </svg>
    </button>

    <transition name="fade">
      <ul
        v-if="open"
        class="absolute mt-1 w-full bg-white border border-gray-200 rounded shadow-lg z-10 overflow-hidden"
      >
        <li
          v-for="option in options"
          :key="option.key"
          @click="select(option)"
        >
          <div class="px-4 py-2 hover:bg-blue-50 hover:text-blue-600 cursor-pointer transition-colors duration-150">
            {{ option.label }}
          </div>
        </li>
      </ul>
    </transition>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount, type Ref } from 'vue'

interface Option { key: string; label: string }

interface DropdownMenuProps {
 options: Option[]
}

defineProps<DropdownMenuProps>()

const emit = defineEmits(['update:selected'])

const open = ref(false)
const selected: Ref<Option | null> = ref(null)
const menuRef: Ref<HTMLElement | null> = ref(null)

function toggle() {
  open.value = !open.value
}

function select(option: Option) {
  selected.value = option
  emit('update:selected', option.key)
  open.value = false
}

function handleClickOutside(event: MouseEvent) {
  if (menuRef.value && !menuRef.value.contains(event.target as HTMLElement)) {
    open.value = false
  }
}

onMounted(() => {
  document.addEventListener('click', handleClickOutside)
})

onBeforeUnmount(() => {
  document.removeEventListener('click', handleClickOutside)
})
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
y
