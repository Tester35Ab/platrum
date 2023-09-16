<script>
export default {
  name: 'v-input',
  props: {
    type: String,
    modelValue: String,
    required: Boolean,
    placeholder: String
  }
}
</script>

<template>
  <input
    :type="type"
    :required="required"
    :value="modelValue ? modelValue : $attrs.value"
    :placeholder="placeholder"
    @input="$emit('input', $event.target.value)"
    class="v-input"
  >
</template>

<style scoped>
.v-input {
  padding: 5px 10px;
  font-size: 16px;
  font-weight: 500;
  border: 1px solid black;
  border-radius: 8px;
  width: 400px;
}

.v-input::placeholder {
  font-weight: 400;
}
</style>
