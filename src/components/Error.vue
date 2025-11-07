<script setup>
  const props = defineProps({
    error: String,
  })

</script>


<template>
  <div v-if="props.error" class="error">
    {{ props.error  }}
  </div>
</template> 

<style scoped>
  .error {
    
    padding: 15px;
    font-size: 18px;
    text-align: center;
    background-color:var(--color-bg-card);
    border-radius: 0 0 25px 25px;
    margin-block-start: -50px;
    margin-block-end: 50px;
  }
</style>  