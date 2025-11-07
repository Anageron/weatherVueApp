<script setup>
import { inject, ref } from "vue";
import Button from "./Button.vue";
import IconNavigation from "./Icons/IconNavigation.vue";
import Input from "./Input.vue";
import { cityProvide } from "../constants";

const city = inject(cityProvide);
const inputValue = ref(city.value);

let isEdited = ref(false);

function select() {
  isEdited.value = false;
  city.value = inputValue.value;
}

function edit() {
  isEdited.value = true;
}
</script>

<template>
  <div class="city-select">
    <Transition name="fade" mode="out-in">
      <Button v-if="!isEdited" @click="edit">
        <IconNavigation />
        Изменить город
      </Button>
      <div v-else class="city-input">
        <Input
          placeholder="Введите город"
          v-model="inputValue"
          v-focus
          @keyup.enter="select"
        />
        <Button @click="select">Сохранить</Button>
      </div>
    </Transition>
  </div>
</template>

<style scoped>
.city-select {
  width: 420px;
}

.city-input {
  display: flex;
  gap: 12px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.25s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
