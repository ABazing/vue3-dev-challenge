<template>
  <div class="resource-card">
    <div class="card-image" :style="{ backgroundImage: `url(${resource.img})` }">
      <div class="card-overlay">
        <span class="material-symbols-outlined category-icon">{{ categoryIcon }}</span>
        <div class="card-actions">
          <span class="material-symbols-outlined">share</span>
          <span class="material-symbols-outlined">more_horiz</span>
          <span
            class="material-symbols-outlined bookmark"
            :class="{ bookmarked: resource.isBookmarked }"
            @click="toggleBookmark(resource.title)"
          >
            {{ resource.isBookmarked ? 'bookmark' : 'bookmark_border' }}
          </span>
        </div>
      </div>
    </div>
    <div class="card-content">
      <p>{{ resource.category }} • Resources</p>
      <h3>{{ resource.title }}</h3>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  resource: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(['toggle-bookmark']);

const categoryIcon = computed(() => {
  switch (props.resource.category) {
    case 'Workplace': return 'work';
    case 'Training': return 'school';
    case 'Productivity': return 'trending_up';
    case 'Education': return 'book';
    default: return 'info';
  }
});

const toggleBookmark = (title) => {
  emit('toggle-bookmark', title);
};
</script>

<style scoped>
.resource-card {
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease;
}

.card-image {
  position: relative;
  height: 150px;
  background-size: cover;
  background-position: center;
  transition: transform 0.3s ease;
}

.resource-card:hover .card-image {
  transform: scale(1.05);
}

.card-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding: 10px;
  background: rgba(0, 0, 0, 0.3);
}

.category-icon {
  color: white;
  font-size: 24px;
}

.card-actions {
  display: flex;
  gap: 10px;
}

.card-actions span {
  color: white;
  font-size: 20px;
  cursor: pointer;
  transition: color 0.2s ease;
}

.card-actions span:hover {
  color: #ddd;
}

.card-actions span:active {
  color: #bbb;
}

.card-actions span:focus-visible {
  outline: 2px solid white;
  outline-offset: 2px;
}

.bookmark.bookmarked {
  color: #1a73e8;
}

.card-content {
  padding: 15px;
  background: #2a2f3b;
  color: white;
}

.card-content p {
  margin: 0 0 5px;
  font-size: 12px;
  color: #ccc;
}

.card-content h3 {
  margin: 0;
  font-size: 16px;
  line-height: 1.4;
}
</style>