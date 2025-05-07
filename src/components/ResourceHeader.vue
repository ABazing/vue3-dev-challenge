<template>
  <div class="header">
    <h1 class="title">Your Resources</h1>
    <div class="actions">
      <button class="action-btn">
        <span class="material-symbols-outlined">edit</span>
      </button>
      <button class="action-btn">
        <span class="material-symbols-outlined">add</span>
      </button>
      <button class="action-btn">
        <span class="material-symbols-outlined">view_list</span>
      </button>
      <button class="action-btn">
        <span class="material-symbols-outlined">view_module</span>
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
// No props or emits needed for this simple component
</script>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 24px;
  padding-bottom: i6px;
  border-bottom: 1px solid #eee;
}

.title {
  font-size: 24px;
  color: #334155;
  margin: 0;
}

.actions {
  display: flex;
  gap: 8px;
}

.action-btn {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: none;
  background: transparent;
  border-radius: 50%;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.action-btn:hover {
  background-color: #f5f5f5;
}

.action-btn:active {
  background-color: #e0e0e0;
}

.action-btn:focus-visible {
  outline: 2px solid #2196F3;
  outline-offset: 2px;
}
</style>
