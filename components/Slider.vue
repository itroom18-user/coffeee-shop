<!-- components/Slider.vue -->
<template>
  <div class="swiper-container">
    <swiper
      :slidesPerView="1"
      :spaceBetween="10"
      :loop="true"
      :autoplay="{ delay: 5000 }"
      :effect="'fade'"
      class="mySwiper"
    >
      <swiper-slide>
        <img
          src="/assets/images/coffee1.jpg"
          alt="Кофе 1"
          class="swiper-image"
        />
      </swiper-slide>
      <swiper-slide>
        <img
          src="/assets/images/coffee2.jpg"
          alt="Кофе 2"
          class="swiper-image"
        />
      </swiper-slide>
      <swiper-slide>
        <img
          src="/assets/images/coffee3.jpg"
          alt="Кофе 3"
          class="swiper-image"
        />
      </swiper-slide>
    </swiper>
  </div>
</template>

<script setup>
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/swiper-bundle.css";
</script>

<style scoped>
.swiper-container {
  width: 100%;
  height: 100%;
  max-height: 500px;
  position: relative;
}

.swiper-image {
  width: 100%;
  object-fit: cover;
  border-radius: 10px;
}
</style>
