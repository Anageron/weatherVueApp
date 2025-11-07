<script setup>
import { computed, inject } from "vue";
import IconNavigation from "./Icons/IconNavigation.vue";
import { cityProvide } from "../constants";
import IconCloud from './Icons/weather/IconCloud.vue';
import IconRain from './Icons/weather/IconRain.vue';
import IconSun from './Icons/weather/IconSun.vue';

const { dayData } = defineProps({
  dayData: Object,
});

const city = inject(cityProvide);

const day = computed(() => {
  return new Date(dayData.date).toLocaleDateString("ru-RU", {
    weekday: "long",
  });
});

const date = computed(() => {
  return new Date(dayData.date).toLocaleDateString("ru-RU", {
    day: "numeric",
    month: "long",
    year: "numeric",
  });
});

const weatherCode = computed(() => {
  return dayData.day.condition.code
})
  
</script>

<template>
  <div class="paneLeft">
    <div>
      <div class="day">
        {{ day }}
      </div>
      <div class="date">
        {{ date }}
      </div>
      <div class="city">
        <IconNavigation />
        {{ city }}
      </div>
    </div>
    <div>
      <div class="weatherIcon">
        <IconSun v-if="weatherCode <= 1003" :size="95" />
        <IconCloud v-if="weatherCode >= 1006 && weatherCode < 1063" :size="95"/>
        <IconRain v-if="weatherCode >= 1063" :size="95"/>
      </div>
      <div class="temp">
        {{ dayData.day.avgtemp_c }}
      </div>
       <div class="condition">
        {{ dayData.day.condition.text }}
      </div>
    </div>
  </div>
</template>

<style scoped>
.paneLeft {
  display: flex;
  flex-direction: column;
  padding: 48px 32px;
  justify-content: space-between;
  height: 100%;
}

.day {
  font-size: 37px;
  font-weight: 700;
  text-transform: capitalize;
  margin-block-end: 16px;
}

.date {
  font-size: 22px;
  font-weight: 500;
  margin-block-end: 10px;
}

.city {
  display: flex;
  gap: 8px;
  align-items: center;
}
.weatherIcon {
  margin-inline-start: 14px;
  margin-block-end: 25px;
}
.temp {
  font-size: 50px;
  font-weight: 700;
  margin-block-end: 10px
}
.condition {
    font-size: 30px;
  font-weight: 700;
}
</style>
