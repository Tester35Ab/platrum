<script>
import VBtn from './UI/VBtn.vue'
export default {
  name: 'Header',
  components: {
    VBtn
  }
}
</script>

<template>
  <header class="header">
    <VBtn @click="$emit('add')" class="add-btn">Добавить</VBtn>
  </header>
</template>

<style scoped>
.header {
  padding: 40px 0;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
