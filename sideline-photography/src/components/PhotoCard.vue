<template>
  <div class="photo-card">
    <img :src="image" :alt="title" class="photo-card__image" />
    <h2 class="photo-card__title">{{ title }}</h2>
    <p class="photo-card__description">{{ description }}</p>
  </div>
</template>

<script setup>
defineProps({
  image: {
    type: String,
    required: true
  },
  title: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: false
  }
});
</script>

