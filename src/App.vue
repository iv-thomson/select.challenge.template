
<script setup lang="ts">
import { ref } from 'vue';
import DropdownMenu from './components/DropdownMenu.vue';

const options = ref([
        { key: 'option-1', label: 'Option 1' },
        { key: 'option-2', label: 'Option 2' },
        { key: 'option-3', label: 'Option 3' },
        { key: 'option-4', label: 'Option 4' },
        { key: 'option-5', label: 'Option 5' },
])
</script>

<template>
  <div class="m-auto w-24 mt-20">
        <dropdown-menu :options="options" />
  </div>
</template>

