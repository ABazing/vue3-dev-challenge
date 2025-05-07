<template>
  <div class="resource-grid">
    <ResourceCard
      v-for="resource in resources"
      :key="resource.title"
      :resource="resource"
      @toggle-bookmark="$emit('toggle-bookmark', resource.title)"
    />
  </div>
</template>

<script setup>
import '../assets/styles/components/ResourceGrid.css';
import ResourceCard from './ResourceCard.vue';

defineProps({
  resources: {
    type: Array,
    required: true
  }
});

defineEmits(['toggle-bookmark']);
</script>
