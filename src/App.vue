<template>
  <div class="resources-app">
    <header>
      <h1>YOUR RESOURCES</h1>
      <div class="header-icons">
        <span class="material-symbols-outlined">edit</span>
        <span class="material-symbols-outlined">add</span>
        <span class="material-symbols-outlined">menu</span>
        <span class="material-symbols-outlined">more_vert</span>
      </div>
    </header>

    <div class="filters">
      <button
        v-for="filter in filters"
        :key="filter"
        :class="{ active: activeFilters.includes(filter) || (filter === 'ALL' && activeFilters.length === filters.length - 1) }"
        @click="toggleFilter(filter)"
      >
        {{ filter }}
      </button>
    </div>

    <div class="resource-grid">
      <ResourceCard
        v-for="resource in filteredResources"
        :key="resource.title"
        :resource="resource"
        @toggle-bookmark="toggleBookmark"
      />
    </div>

    <button class="show-more">SHOW MORE</button>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import ResourceCard from './components/ResourceCard.vue';

const resources = ref([
  {
    title: "Ignition Podcast: Innovation, Agility, Talent, Workplace, Culture, and more",
    category: "Workplace",
    isBookmarked: true,
    img: "workplace",
  },
  {
    title: "Threat Briefing",
    category: "Training",
    isBookmarked: false,
    img: "training",
  },
  {
    title: "SSC Telework Portal",
    category: "Productivity",
    isBookmarked: false,
    img: "productivity",
  },
  {
    title: "AIR FORCE Virtual Education",
    category: "Education",
    isBookmarked: false,
    img: "virtual-education",
  },
  {
    title: "Guide to DigitalU",
    category: "Education",
    isBookmarked: true,
    img: "education",
  },
  {
    title: "How Build a Collaborative Team Environment",
    category: "Workplace",
    isBookmarked: false,
    img: "team-environment",
  },
]);

const filters = ['ALL', 'ACQUISITION', 'COMMUNICATION', 'ENGINEERING', 'EDUCATION', 'PRODUCTIVITY', 'TRAINING', 'WORKPLACE'];
const activeFilters = ref(['ALL']);

const filteredResources = computed(() => {
  if (activeFilters.value.includes('ALL') || activeFilters.value.length === filters.length - 1) {
    return resources.value;
  }
  return resources.value.filter(resource => activeFilters.value.includes(resource.category));
});

const toggleFilter = (filter) => {
  if (filter === 'ALL') {
    activeFilters.value = ['ALL'];
  } else {
    if (activeFilters.value.includes('ALL')) {
      activeFilters.value = [];
    }
    if (activeFilters.value.includes(filter)) {
      activeFilters.value = activeFilters.value.filter(f => f !== filter);
    } else {
      activeFilters.value.push(filter);
    }
    if (activeFilters.value.length === 0) {
      activeFilters.value = ['ALL'];
    } else if (activeFilters.value.length === filters.length - 1) {
      activeFilters.value = ['ALL'];
    }
  }
};

const toggleBookmark = (title) => {
  const resource = resources.value.find(r => r.title === title);
  if (resource) {
    resource.isBookmarked = !resource.isBookmarked;
  }
};
</script>

<style scoped>
.resources-app {
  font-family: Arial, sans-serif;
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

h1 {
  color: #1a73e8;
  font-size: 24px;
  margin: 0;
}

.header-icons span {
  font-size: 24px;
  margin-left: 15px;
  cursor: pointer;
  color: #666;
}

.header-icons span:hover {
  color: #333;
}

.filters {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.filters button {
  padding: 8px 16px;
  border: 1px solid #ccc;
  border-radius: 20px;
  background: white;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.2s ease;
}

.filters button.active {
  background: #1a73e8;
  color: white;
  border-color: #1a73e8;
}

.filters button:hover {
  background: #e8f0fe;
}

.filters button:active {
  background: #d2e3fc;
}

.filters button:focus-visible {
  outline: 2px solid #1a73e8;
  outline-offset: 2px;
}

.resource-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
  margin-bottom: 20px;
}

.show-more {
  display: block;
  margin: 0 auto;
  padding: 10px 20px;
  border: 1px solid #ccc;
  border-radius: 20px;
  background: white;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.2s ease;
}

.show-more:hover {
  background: #e8f0fe;
}

.show-more:active {
  background: #d2e3fc;
}

.show-more:focus-visible {
  outline: 2px solid #1a73e8;
  outline-offset: 2px;
}
</style>