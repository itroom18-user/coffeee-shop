<!-- app.vue -->
<template>
  <div>
    <NuxtPage />
  </div>
</template>

<script setup>
import { onMounted } from "vue";
import { useRouter } from "vue-router";

// Перенаправление на главную страницу при загрузке
const router = useRouter();

onMounted(() => {
  // Перенаправление на главную страницу, если текущий путь не /home
  if (router.currentRoute.value.path !== "/") {
    router.push("/");
  }
});
</script>
