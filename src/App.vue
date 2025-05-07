<template>
  <div class="app-container">
    <header>
      <div class="header-content">
        <h1>Your Resources</h1>
        <div class="header-actions">
          <button class="icon-button"><span class="material-symbols-outlined">edit</span></button>
          <button class="icon-button"><span class="material-symbols-outlined">add</span></button>
          <button class="icon-button"><span class="material-symbols-outlined">view_list</span></button>
          <button class="icon-button"><span class="material-symbols-outlined">apps</span></button>
        </div>
      </div>
      <p>View and bookmark resources</p>

      <FilterButtons
        :selectedCategories="selectedCategories"
        @update:selectedCategories="selectedCategories = $event"
      />
    </header>

    <main>
      <ResourceGrid
        :resources="filteredResources"
        @toggle-bookmark="toggleBookmark"
      />
    </main>

    <div class="show-more">
      <button class="show-more-button">
        <span class="material-symbols-outlined">refresh</span>
        Show More
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import FilterButtons from './components/FilterButtons.vue';
import ResourceGrid from './components/ResourceGrid.vue';
import resources from './data/resources';

import './assets/styles/variables.css';
import './assets/styles/global.css';
import './assets/styles/app.css';

const allResources = ref(resources);
const selectedCategories = ref(['All']);

const filteredResources = computed(() => {
  if (selectedCategories.value.includes('All')) {
    return allResources.value;
  }

  return allResources.value.filter(resource =>
    selectedCategories.value.includes(resource.category)
  );
});

const toggleBookmark = (resourceTitle) => {
  const resource = allResources.value.find(r => r.title === resourceTitle);
  if (resource) {
    resource.isBookmarked = !resource.isBookmarked;
  }
};
</script>
