<script setup>
import Button from "./components/Button.vue";
import CitySelect from "./components/CitySelect.vue";
import Stat from "./components/Stat.vue";

const data = {
  label: "Важность",
  stat: "90%",
}

function getCity(city) {
  console.log(city)
}

</script>

<template>
  <main class="main">
    <Stat v-bind="data" />
    <Stat v-bind="data" />
    <CitySelect @select-city="getCity" />
  </main>
</template>

<style scoped>
.main {
  padding: 50px 60px;
  background-color: var(--color-bg-main);
  border-radius: 25px;
}

.main__input {
  display: flex;
  gap: 12px;
}
</style>
