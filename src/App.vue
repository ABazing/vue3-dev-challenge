<template>
  <div class="app-container">
    <ResourceHeader />
    <ResourceFilter @filter-change="handleFilterChange" />

    <div class="resources-grid">
      <ResourceCard
        v-for="resource in filteredResources"
        :key="resource.title"
        :resource="resource"
        @toggle-bookmark="toggleBookmark"
      />
    </div>

    <div class="show-more">
      <button class="show-more-btn">
        <span class="material-symbols-outlined">add_circle_outline</span>
        Show More
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import ResourceHeader from './components/ResourceHeader.vue';
import ResourceFilter from './components/ResourceFilter.vue';
import ResourceCard from './components/ResourceCard.vue';
import resourcesData from './data/resources';

interface Resource {
  title: string;
  category: string;
  isBookmarked: boolean;
  img: string;
}

const resources = ref<Resource[]>(resourcesData);
const activeFilters = ref<string[]>(['All']);

const handleFilterChange = (filters: string[]) => {
  activeFilters.value = filters;
};

const filteredResources = computed(() => {
  if (activeFilters.value.includes('All')) {
    return resources.value;
  }

  return resources.value.filter(resource =>
    activeFilters.value.includes(resource.category)
  );
});

const toggleBookmark = (resource: Resource) => {
  const index = resources.value.findIndex(r => r.title === resource.title);
  if (index !== -1) {
    resources.value[index].isBookmarked = !resources.value[index].isBookmarked;
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,0..200');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Roboto', sans-serif;
  background-color: #f9f9f9;
  color: #333;
}

.app-container {
  max-width: 1200px;
  margin: 40px auto;
  padding: 0 20px;
}

.resources-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 20px;
  margin-bottom: 30px;
}

.show-more {
  display: flex;
  justify-content: center;
  margin: 30px 0;
}

.show-more-btn {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 16px;
  border-radius: 20px;
  border: none;
  background-color: transparent;
  cursor: pointer;
  font-size: 14px;
  color: #666;
  transition: background-color 0.2s ease;
}

.show-more-btn:hover {
  background-color: #f0f0f0;
}

.show-more-btn:focus-visible {
  outline: 2px solid #2196F3;
  outline-offset: 2px;
}

.material-symbols-outlined {
  font-variation-settings:
  'FILL' 0,
  'wght' 400,
  'GRAD' 0,
  'opsz' 24;
}

</style>
