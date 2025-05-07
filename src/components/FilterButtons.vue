<template>
  <div class="filter-container">
    <button
      class="filter-button"
      :class="{ active: isActive('All') }"
      @click="toggleFilter('All')"
    >
      ALL
    </button>
    <button
      class="filter-button"
      :class="{ active: isActive('Acquisition') }"
      @click="toggleFilter('Acquisition')"
    >
      Acquisition
    </button>
    <button
      class="filter-button"
      :class="{ active: isActive('Communication') }"
      @click="toggleFilter('Communication')"
    >
      Communication
    </button>
    <button
      class="filter-button"
      :class="{ active: isActive('Engineering') }"
      @click="toggleFilter('Engineering')"
    >
      Engineering
    </button>
    <button
      class="filter-button"
      :class="{ active: isActive('Education') }"
      @click="toggleFilter('Education')"
    >
      Education
    </button>
    <button
      class="filter-button"
      :class="{ active: isActive('Productivity') }"
      @click="toggleFilter('Productivity')"
    >
      Productivity
    </button>
    <button
      class="filter-button"
      :class="{ active: isActive('Training') }"
      @click="toggleFilter('Training')"
    >
      Training
    </button>
    <button
      class="filter-button"
      :class="{ active: isActive('Workplace') }"
      @click="toggleFilter('Workplace')"
    >
      Workplace
    </button>
  </div>
</template>

<script setup>
import { computed } from 'vue';
import '../assets/styles/components/FilterButtons.css';

const props = defineProps({
  selectedCategories: {
    type: Array,
    required: true
  }
});

const emit = defineEmits(['update:selectedCategories']);

const allCategories = [
  'Acquisition', 'Communication', 'Engineering',
  'Education', 'Productivity', 'Training', 'Workplace'
];

const isActive = (category) => {
  return props.selectedCategories.includes(category);
};

const toggleFilter = (category) => {
  let newSelectedCategories = [...props.selectedCategories];

  if (category === 'All') {
    newSelectedCategories = ['All'];
  } else {
    newSelectedCategories = newSelectedCategories.filter(c => c !== 'All');

    if (newSelectedCategories.includes(category)) {
      newSelectedCategories = newSelectedCategories.filter(c => c !== category);
    } else {
      newSelectedCategories.push(category);
    }

    if (newSelectedCategories.length === 7) {
      newSelectedCategories = ['All'];
    }

    if (newSelectedCategories.length === 0) {
      newSelectedCategories = ['All'];
    }
  }

  emit('update:selectedCategories', newSelectedCategories);
};
</script>
