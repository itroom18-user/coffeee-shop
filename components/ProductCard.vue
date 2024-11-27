<!-- components/ProductCard.vue -->
<template>
  <div class="product-card">
    <img :src="image" alt="product image" class="product-image" />
    <h3>{{ title }}</h3>
    <p class="product-price">{{ price }}₽</p>
    <p class="product-description">{{ description }}</p>
    <router-link :to="`/product/${id}`" class="btn">Подробнее</router-link>
  </div>
</template>

<script setup>
defineProps({
  id: Number,
  image: String,
  title: String,
  price: Number,
  description: String,
});
</script>

<style scoped>
.product-card {
  background-color: #f5f1e1;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.product-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
}

.product-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 8px;
}

.product-title {
  font-size: 1.5em;
  color: #3e2b1d;
}

.product-price {
  color: #ad8c62;
  font-weight: bold;
}

.product-description {
  color: #7d6e4e;
  font-size: 0.9em;
}
</style>
