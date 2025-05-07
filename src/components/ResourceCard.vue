<template>
  <div class="resource-card">
    <div class="image-container">
      <img :src="getImageUrl(resource.img)" :alt="resource.title">
      <div class="card-actions">
        <button
          class="bookmark-button"
          :class="{ active: resource.isBookmarked }"
          @click="$emit('toggle-bookmark', resource.title)"
        >
          <span class="material-symbols-outlined">
            {{ resource.isBookmarked ? 'bookmark' : 'bookmark_border' }}
          </span>
        </button>
        <button class="more-button">
          <span class="material-symbols-outlined">more_vert</span>
        </button>
      </div>
      <div class="category-label">
        <span class="material-symbols-outlined">lightbulb</span>
        <span>{{ resource.category }}</span>
        <span class="dot-separator">•</span>
        <span>Resources</span>
      </div>
    </div>
    <div class="card-content">
      <h3>{{ resource.title }}</h3>
    </div>
  </div>
</template>

<script setup>
import '../assets/styles/components/ResourceCard.css';

const props = defineProps({
  resource: {
    type: Object,
    required: true
  }
});

defineEmits(['toggle-bookmark']);

const getImageUrl = (imageName) => {
  try {
    return new URL(`../assets/images/${imageName}.jpg`, import.meta.url).href;
  } catch (error) {
    console.error(`Image not found: ${imageName}`);
    return '';
  }
};
</script>
