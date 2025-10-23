<script setup>

</script>

<template>
  <input class="input" />
</template>

<style scoped>
  .input{
    border: none;
    border-radius: 10px;
    background-color: var(--color-bg-card);
    box-shadow: 1px 2px 4px 0px var(--color-bg-main);
    color: var(--color-primary);
    font-size: 18px;
    font-weight: 400;
    padding: 15px 20px;
  }

  .input::placeholder{
    color: var(--color-text-placeholder);
  }
</style>