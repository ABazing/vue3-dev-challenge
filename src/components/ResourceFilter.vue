<template>
  <div class="filter-container">
    <div class="filter-text">View and bookmark resources</div>
    <div class="filter-buttons">
      <button
        class="filter-btn"
        :class="{ active: activeFilters.includes('All') }"
        @click="toggleFilter('All')"
      >
        ALL
      </button>
      <button
        v-for="category in categories"
        :key="category"
        class="filter-btn"
        :class="{ active: activeFilters.includes(category) }"
        @click="toggleFilter(category)"
      >
        {{ category }}
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, defineEmits, watch } from 'vue';

const categories = ['Acquisition', 'Communication', 'Engineering', 'Education', 'Productivity', 'Training', 'Workplace'];
const activeFilters = ref<string[]>(['All']);
const emit = defineEmits(['filter-change']);

const toggleFilter = (filter: string) => {
  if (filter === 'All') {
    activeFilters.value = ['All'];
  } else {
    // Remove 'All' if it's present
    const allIndex = activeFilters.value.indexOf('All');
    if (allIndex !== -1) {
      activeFilters.value.splice(allIndex, 1);
    }

    // Toggle the selected filter
    const index = activeFilters.value.indexOf(filter);
    if (index === -1) {
      activeFilters.value.push(filter);
    } else {
      activeFilters.value.splice(index, 1);
    }

    // If all individual filters are selected or none are selected, switch to 'All'
    if (activeFilters.value.length === categories.length || activeFilters.value.length === 0) {
      activeFilters.value = ['All'];
    }
  }

  emit('filter-change', activeFilters.value);
};

// Initial emit
watch(activeFilters, (newVal) => {
  emit('filter-change', newVal);
}, { immediate: true });
</script>

<style scoped>
.filter-container {
  margin-bottom: 20px;
}

.filter-text {
  color: #666;
  margin-bottom: 12px;
  font-size: 14px;
}

.filter-buttons {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.filter-btn {
  padding: 6px 16px;
  border-radius: 20px;
  border: 1px solid #e0e0e0;
  background-color: #fff;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.2s ease;
  color: #666;
}

.filter-btn:hover {
  background-color: #f5f5f5;
}

.filter-btn:active {
  background-color: #e0e0e0;
}

.filter-btn:focus-visible {
  outline: 2px solid #2196F3;
  outline-offset: 2px;
}

.filter-btn.active {
  background-color: #2196F3;
  color: white;
  border-color: #2196F3;
}

.filter-btn.active:hover {
  background-color: #1976D2;
}
</style>
