<script setup>
import { computed } from 'vue';
import IconCloud from './Icons/weather/IconCloud.vue';
import IconRain from './Icons/weather/IconRain.vue';
import IconSun from './Icons/weather/IconSun.vue';

const {weatherCode, temperature, date, isActive} = defineProps({
  weatherCode: Number,
  temperature: Number,
  date: Date,
  isActive: Boolean,
})
let iconColor = computed(() => isActive ? 'var(--color-primary-inverted)' : 'var(--color-primary)')
</script>

<template>
  <button class="day-card" :class="{active: isActive}">
    <IconSun v-if="weatherCode <= 1003" :color="iconColor"/>
    <IconCloud v-if="weatherCode >= 1006 && weatherCode < 1063" :color="iconColor"/>
    <IconRain v-if="weatherCode >= 1063" :color="iconColor"/>
    <div class="day-card__day">
      {{ date.toLocaleDateString('ru-RU', { weekday:'short'}) }}
    </div>
    <div class="day-card__temp">
      {{ temperature }} °C
    </div>
  </button>
</template>

<style scoped>
.day-card {
  width: 100%;
  color: var(--color-primary);
  padding: 20px 24px;
  background-color: var(--color-bg-card);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 15px;
  font-size: 20px;
  border: none;
  cursor: pointer;
  border-radius: 10px;
  box-shadow: 1px 2px 4px 0 #222831;
}

.active {
  background-color: var(--color-primary);
  color: var(--color-primary-inverted);
}

.day-card:not(.active):hover {
  background-color:#3a434f;
}

.day-card__temp {
  font-weight: 700;
}


</style>