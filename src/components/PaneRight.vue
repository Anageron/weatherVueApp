<script setup>
import { computed } from 'vue';
import Error from './Error.vue';
import DayCard from './DayCard.vue';
import CitySelect from './CitySelect.vue';
import Stat from './Stat.vue';
import { errorMap } from '../constants';

const {error, data, activeIndex} = defineProps({
  error: Object,
  data: Object,
  activeIndex: Number
})

const emit = defineEmits(['select-index', 'select-city'])



const statData = computed(() => {
  return [
    {
      label: "Влажность",
      stat: data.forecast.forecastday[activeIndex].day.avghumidity + " %",
    },
    {
      label: "Вероятность дождя",
      stat: data.forecast.forecastday[activeIndex].day.daily_chance_of_rain + " %",
    },
    {
      label: "Ветер",
      stat: data.forecast.forecastday[activeIndex].day.maxwind_kph + " км/ч",
    },
  ];
});

const errorDisplay = computed(() => {
  if (!error.value) return null;
  return errorMap.get(error.error?.code);
});
</script>

<template>
      <Error v-if="error" :error="errorDisplay" />
      <div v-if="data" class="stat-data">
        <div class="stat-list">
          <Stat v-for="data in statData" :key="data.label" v-bind="data" />
        </div>
        <div class="daycard-list">
          <DayCard v-for="(item, index) in data.forecast.forecastday" 
          :key="item.date"
          :weather-code="item.day.condition.code" 
          :temperature="item.day.avgtemp_c" 
          :date="new Date(item.date)"
          :is-active="activeIndex == index"
          @click="() => (emit('select-index', index))"
          />
        </div>
      </div>

      <CitySelect  />
 
</template>

<style scoped>
.daycard-list {
  display: flex;
  gap: 1px;
}

.list {
  display: flex;
  flex-direction: column;
  gap: 24px;
  list-style: none;
}

.stat-data {
  display: flex;
  flex-direction: column;
  gap: 80px;
  margin-block-end: 70px;
}

.stat-list{
  display: flex;
  flex-direction: column;
  gap: 16px;
}
</style>