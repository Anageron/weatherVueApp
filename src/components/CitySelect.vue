<script setup>
import { ref } from "vue";
import Button from "./Button.vue";
import IconNavigation from "./Icons/IconNavigation.vue";
import Input from "./Input.vue";
 
const emit = defineEmits({
  selectCity(payload){
            return payload;
    },
  });

let isEdited = ref(false);


function select() {
  isEdited.value = false;
  console.log(isEdited.value) 
  emit('selectCity', 'London');
}

function edit() {
  isEdited.value = true;
}

</script>

<template>
  <Button v-show="!isEdited" @click="edit" >
    <IconNavigation />
    Изменить город
  </Button>
  <div v-show="isEdited">
    <Input placeholder="Введите город"/>
    <Button @click="select">Сохранить</Button>
  </div>
</template>

<script></script>