<template>
  <div class="menu-page">
    <Header />
    <h2>Наше меню</h2>
    <div class="menu-categories">
      <!-- Кнопка для Напитков -->
      <router-link to="/menu/drinks" class="menu-item drinks">
        <div class="menu-overlay">
          <h3>Напитки</h3>
        </div>
      </router-link>

      <!-- Кнопка для Закусок -->
      <router-link to="/menu/snacks" class="menu-item snacks">
        <div class="menu-overlay">
          <h3>Закуски</h3>
        </div>
      </router-link>

      <!-- Кнопка для Десертов -->
      <router-link to="/menu/desserts" class="menu-item desserts">
        <div class="menu-overlay">
          <h3>Десерты</h3>
        </div>
      </router-link>
    </div>
    <Footer />
  </div>
</template>

<script setup>
import Header from "~/components/Header.vue";
import Footer from "~/components/Footer.vue";
</script>

<style scoped>
.menu-page {
  padding: 20px;
  text-align: center;
  background-color: #daad6b;
}

h2 {
  font-size: 2rem;
  color: #3e2b1d;
  margin-bottom: 20px;
}

.menu-categories {
  display: flex;
  justify-content: space-between;
  gap: 10px;
  height: 100vh; /* Занимает всю высоту экрана */
}

.menu-item {
  position: relative;
  display: block;
  width: 32%; /* Каждая кнопка занимает 1/3 ширины */
  height: 100%; /* Кнопки растягиваются по высоте */
  border-radius: 5px;
  overflow: hidden;
  text-decoration: none;
}

.menu-item .menu-overlay {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: white;
  text-align: center;
  background-color: rgba(0, 0, 0, 0.5); /* Полупрозрачный фон */
  padding: 10px 20px;
  border-radius: 5px;
}

.menu-item h3 {
  font-size: 2rem;
  font-weight: 700;
  margin: 0;
}

/* Стили для кнопок с изображениями */
.menu-item.drinks {
  background-image: url("assets/images/coffee1.jpg");
  background-size: cover;
  background-position: center;
}

.menu-item.snacks {
  background-image: url("assets/images/cakes1.jpg");
  background-size: cover;
  background-position: center;
}

.menu-item.desserts {
  background-image: url("assets/images/dessert1.jpg");
  background-size: cover;
  background-position: center;
}

/* Эффект при наведении */
.menu-item:hover {
  transform: scale(1.05); /* Увеличение кнопки при наведении */
}

.menu-item:hover .menu-overlay {
  background-color: rgba(0, 0, 0, 0.7); /* Темнее фон при наведении */
}
</style>
