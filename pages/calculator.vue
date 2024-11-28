<template>
  <div class="calculator-page">
    <Header />

    <!-- Основной контейнер калькулятора -->
    <section class="calculator-container" data-aos="fade-up">
      <div class="container">
        <h1>Соберите свой заказ</h1>

        <!-- Шаг 1: Выбор стакана -->
        <div class="step">
          <h2>Выберите стакан</h2>
          <div class="glass-options">
            <div
              v-for="glass in glasses"
              :key="glass.id"
              class="glass-option"
              :class="{ active: selectedGlass === glass.id }"
              @click="selectGlass(glass.id)"
            >
              <img :src="glass.image" :alt="glass.name" />
              <p>{{ glass.name }}</p>
            </div>
          </div>
        </div>

        <!-- Шаг 2: Выбор напитка -->
        <div class="step" v-if="selectedGlass">
          <h2>Выберите напиток</h2>
          <div class="drink-options">
            <div
              v-for="drink in drinks"
              :key="drink.id"
              class="drink-option"
              :class="{ active: selectedDrink === drink.id }"
              @click="selectDrink(drink.id)"
            >
              <img :src="drink.image" :alt="drink.name" />
              <p>{{ drink.name }}</p>
            </div>
          </div>
        </div>

        <!-- Шаг 3: С собой или в кофейне -->
        <div class="step" v-if="selectedDrink">
          <h2>Хотите с собой или в кофейне?</h2>
          <div class="options">
            <button :class="{ active: isToGo }" @click="selectOption('toGo')">
              С собой
            </button>
            <button
              :class="{ active: !isToGo }"
              @click="selectOption('inCafe')"
            >
              В кофейне
            </button>
          </div>
        </div>

        <!-- Шаг 4: Добавки -->
        <div class="step" v-if="isToGo !== null">
          <h2>Выберите добавки</h2>
          <div class="add-ons">
            <div
              v-for="addon in addOns"
              :key="addon.id"
              class="addon-option"
              :class="{ active: selectedAddOns.includes(addon.id) }"
              @click="toggleAddOn(addon.id)"
            >
              <p>{{ addon.name }}</p>
            </div>
          </div>
        </div>

        <!-- Шаг 5: Подтверждение заказа -->
        <div class="step" v-if="selectedAddOns.length > 0 || isToGo !== null">
          <button class="confirm-button" @click="confirmOrder">
            Сделать заказ
          </button>
        </div>
      </div>
    </section>

    <!-- Анимация заказа (пакет или стол) -->
    <div v-if="orderConfirmed" class="order-animation">
      <div class="order-content">
        <img v-if="isToGo" src="assets/images/package.png" alt="Пакет" />
        <div v-else class="order-table">Ваш заказ на столе</div>
        <div class="order-details">
          <h3>Ваш заказ:</h3>
          <p>Стакан: {{ selectedGlassName }}</p>
          <p>Напиток: {{ selectedDrinkName }}</p>
          <p>Добавки: {{ selectedAddOnsNames.join(", ") }}</p>
        </div>
      </div>
    </div>

    <Footer />
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import Header from "~/components/Header.vue";
import Footer from "~/components/Footer.vue";
import AOS from "aos";
import "aos/dist/aos.css";

const glasses = [
  { id: 1, name: "Маленький стакан", image: "assets/images/small.png" },
  { id: 2, name: "Средний стакан", image: "assets/images/medium.png" },
  { id: 3, name: "Большой стакан", image: "assets/images/large.png" },
];

const drinks = [
  { id: 1, name: "Кофе", image: "assets/images/coffee.jpg" },
  { id: 2, name: "Сок", image: "assets/images/juice.jpg" },
  { id: 3, name: "Чай", image: "assets/images/tea.jpg" },
];

const addOns = [
  { id: 1, name: "Молоко", image: "" },
  { id: 2, name: "Сироп", image: "" },
  { id: 3, name: "Шоколад", image: "" },
];

const selectedGlass = ref(null);
const selectedDrink = ref(null);
const isToGo = ref(null);
const selectedAddOns = ref([]);

const orderConfirmed = ref(false);

const selectGlass = (id) => {
  selectedGlass.value = id;
};

const selectDrink = (id) => {
  selectedDrink.value = id;
};

const selectOption = (option) => {
  isToGo.value = option === "toGo";
};

const toggleAddOn = (id) => {
  if (selectedAddOns.value.includes(id)) {
    selectedAddOns.value = selectedAddOns.value.filter((addon) => addon !== id);
  } else {
    selectedAddOns.value.push(id);
  }
};

const confirmOrder = () => {
  orderConfirmed.value = true;
};

const selectedGlassName = computed(() => {
  const glass = glasses.find((g) => g.id === selectedGlass.value);
  return glass ? glass.name : "";
});

const selectedDrinkName = computed(() => {
  const drink = drinks.find((d) => d.id === selectedDrink.value);
  return drink ? drink.name : "";
});

const selectedAddOnsNames = computed(() => {
  return selectedAddOns.value
    .map((id) => {
      const addon = addOns.find((a) => a.id === id);
      return addon ? addon.name : "";
    })
    .filter(Boolean);
});

onMounted(() => {
  AOS.init({
    duration: 1000,
    once: true,
  });
});
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;700&family=Lora:wght@400;700&display=swap");

.calculator-page {
  font-family: "Lora", serif;
  background-color: #f8f5eb;
  padding-bottom: 40px;
}

h1 {
  text-align: center;
  font-family: "Dancing Script", cursive;
  font-size: 3rem;
}

.step {
  padding: 40px 0;
  text-align: center;
}

.glass-options,
.drink-options,
.add-ons {
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
}

.glass-option,
.drink-option,
.addon-option {
  cursor: pointer;
  transition: transform 0.3s ease;
}

.glass-option img,
.drink-option img {
  width: 150px;
  height: 150px;
  object-fit: cover;
  border-radius: 10px;
}

.glass-option p,
.drink-option p,
.addon-option p {
  margin-top: 10px;
  font-size: 1.1rem;
}

.glass-option.active,
.drink-option.active,
.addon-option.active {
  transform: scale(1.1);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.options button {
  padding: 10px 20px;
  font-size: 1.2rem;
  margin: 0 10px;
  background-color: #cca763;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

.options button.active {
  background-color: #ad8c62;
}

.confirm-button {
  padding: 15px 30px;
  background-color: #cca763;
  color: white;
  font-size: 1.5rem;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  transition: background-color 0.3s;
}

.confirm-button:hover {
  background-color: #ad8c62;
}

/* Анимация для заказа */
.order-animation {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: rgba(0, 0, 0, 0.7);
  padding: 40px;
  border-radius: 10px;
  text-align: center;
  color: white;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
}

.order-content img {
  width: 150px;
  height: 150px;
  margin-bottom: 20px;
}

.order-table {
  font-size: 1.5rem;
  color: #cca763;
}

.order-details {
  margin-top: 20px;
}

.order-details h3 {
  font-size: 1.5rem;
  font-weight: bold;
}

.order-details p {
  font-size: 1.2rem;
}
</style>
