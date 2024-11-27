<!-- components/Header.vue -->
<template>
  <header>
    <div class="logo">
      <router-link to="/">
        <img
          src="assets/images/logo.png"
          alt="Lakrica Coffee"
          class="logo-img"
        />
      </router-link>
    </div>
    <nav>
      <router-link to="/" class="nav-item">Главная</router-link>
      <router-link to="/menu" class="nav-item">Меню</router-link>
      <router-link to="/about" class="nav-item">О нас</router-link>
      <router-link to="/contact" class="nav-item">Контакты</router-link>
    </nav>
  </header>
</template>

<script setup></script>

<style scoped>
header {
  background-color: var(--light-coffee);
  padding: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo img {
  width: 150px;
}

nav {
  display: flex;
  gap: 30px;
}

.nav-item {
  color: var(--coffee-brown);
  font-size: 1.2rem;
  text-decoration: none;
  position: relative; /* Для создания эффекта подчеркивания */
  transition: color 0.3s ease, text-decoration 0.3s ease;
}

.nav-item:hover {
  color: var(--golden-beige);
  text-decoration: underline; /* Подчеркивание при наведении */
}

.nav-item::after {
  content: ""; /* Псевдоэлемент для дополнительного стилизования */
  position: absolute;
  bottom: -5px; /* Расстояние от текста */
  left: 0;
  width: 100%;
  height: 2px; /* Толщина подчеркивания */
  background-color: var(--golden-beige); /* Цвет подчеркивания */
  transform: scaleX(0); /* Начальная скрытая позиция */
  transform-origin: bottom right;
  transition: transform 0.3s ease;
}

.nav-item:hover::after {
  transform: scaleX(1); /* Эффект появления линии подчеркивания */
  transform-origin: bottom left;
}
</style>
