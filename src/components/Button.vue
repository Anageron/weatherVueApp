<script setup>

</script>

<template>
  <button class="button">
    <slot/>
  </button>
</template>

<style scoped>
  .button {
    display: flex;
    width: 100%;
    gap: 9px;
    align-items: center;
    border: none;
    border-radius: 10px;
    background: var(--gradient);
    padding: 14px;
    font-family: var(--font);
    font-size: 20px;
    font-weight: 600;
    color: var(--color-primary);
    cursor: pointer;
    justify-content: center;
  }

  .button:hover {
    background: var(--gradient-inverted);
  }
</style>