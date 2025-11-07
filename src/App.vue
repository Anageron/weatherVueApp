<script setup>
import { onMounted, provide, ref, watch } from "vue";
import PaneRight from "./components/PaneRight.vue";
import { API_ENDPOINT, cityProvide } from "./constants";
import PaneLeft from "./components/PaneLeft.vue";


let data = ref();
let error = ref();
let activeIndex = ref(0);
let city = ref("Moscow");

provide(cityProvide, city);

watch(city, () => {
  getCity(city.value)
})

onMounted(() => {
   getCity(city.value)
})

async function getCity(city) {
  const params = new URLSearchParams({
    q: city,
    lang: "ru",
    key: "bfb715b457fb4633995154136252710",
    days: 3,
  });

  const res = await fetch(`${API_ENDPOINT}/forecast.json?${params.toString()}`);
  if (res.status !== 200) {
    error.value = await res.json();
    data.value = null;
    return;
  }
  error.value = null;
  data.value = await res.json();
}
</script>

<template>
  <main class="main">
    <div class="left">
      <PaneLeft
        v-if="data"
        :dayData="data.forecast.forecastday[activeIndex]"
      />
    </div>
    <div class="right">
      <PaneRight 
        :data 
        :error
        :active-index="activeIndex"
        @select-index="(i) => activeIndex = i"
      />
    </div>

  </main>
</template>

<style scoped>

.main {
  display: flex;
  align-items: center;
  justify-content: center;
}


.right {
  width: 555px;
  padding: 50px 60px;
  background-color: var(--color-bg-main);
  border-radius: 0 25px 25px 0;
}

.left {
  width:500px;
  height: 680px;
  border-radius: 30px;
  background-image: url(/public/left.png);
  background-repeat: no-repeat;
  background-size: cover;
}

</style>
