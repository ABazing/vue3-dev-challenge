<template>
  <div class="card">
    <div class="card-image">
      <img :src="`/src/assets/images/${resource.img}.jpg`" :alt="resource.title">
    </div>
    <div class="card-content">
      <div class="card-category">
        <span class="category-icon">
          <span class="material-symbols-outlined">
            {{ getCategoryIcon(resource.category) }}
          </span>
        </span>
        <span class="category-text">{{ resource.category }} • Resources</span>
      </div>
      <h3 class="card-title">{{ resource.title }}</h3>
    </div>
    <div class="card-actions">
      <button
        class="bookmark-btn"
        :class="{ 'bookmarked': resource.isBookmarked }"
        @click="toggleBookmark"
      >
        <span class="material-symbols-outlined">
          {{ resource.isBookmarked ? 'bookmark' : 'bookmark_border' }}
        </span>
      </button>
      <button class="more-btn">
        <span class="material-symbols-outlined">more_vert</span>
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  resource: {
    type: Object,
    required: true
  }
});

const emit = defineEmits(['toggle-bookmark']);

const toggleBookmark = () => {
  emit('toggle-bookmark', props.resource);
};

const getCategoryIcon = (category: string) => {
  switch(category) {
    case 'Workplace':
      return 'business';
    case 'Training':
      return 'school';
    case 'Productivity':
      return 'laptop';
    case 'Education':
      return 'menu_book';
    default:
      return 'article';
  }
};
</script>

<style scoped>
.card {
  position: relative;
  border-radius: 8px;
  overflow: hidden;
  background-color: #fff;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
  margin-bottom: 20px;
}

.card:hover .card-image img {
  transform: scale(1.05);
}

.card-image {
  height: 150px;
  overflow: hidden;
}

.card-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.card-content {
  padding: 16px;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.7), transparent);
  color: white;
}

.card-category {
  display: flex;
  align-items: center;
  font-size: 12px;
  margin-bottom: 4px;
}

.category-icon {
  display: flex;
  align-items: center;
  margin-right: 4px;
}

.card-title {
  font-size: 16px;
  margin: 0;
  line-height: 1.3;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-box-orient: vertical;
}

.card-actions {
  position: absolute;
  top: 8px;
  right: 8px;
  display: flex;
  gap: 4px;
}

.bookmark-btn, .more-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  border: none;
  background-color: rgba(255, 255, 255, 0.8);
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.bookmark-btn:hover, .more-btn:hover {
  background-color: rgba(255, 255, 255, 1);
}

.bookmark-btn:focus-visible, .more-btn:focus-visible {
  outline: 2px solid #2196F3;
  outline-offset: 2px;
}

.bookmark-btn.bookmarked .material-symbols-outlined {
  color: #2196F3;
}

.material-symbols-outlined {
  font-size: 20px;
}
</style>
