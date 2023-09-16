<script>
export default {
  name: 'VBtn',
  props: {
    disabled: Boolean,
    type: String
  }
}
</script>

<template>
<button class="v-btn" @click="$emit('click')" :disabled="disabled" :type="type">
  <slot></slot>
</button>
</template>

<style scoped>
.v-btn {
  padding: 10px 25px;
  border-radius: 8px;
  background-color: #1BA4C0;
  font-size: 16px;
  color: white;
  cursor: pointer;
  transition: background-color .25s ease-in;
}

.v-btn:hover {
  background-color: #0C8DA7;
}
</style>
