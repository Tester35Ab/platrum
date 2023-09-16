<script>
import CloseIcon from '@/components/UI/icons/CloseIcon.vue'

export default {
  name: 'Modal',
  components: {
    CloseIcon
  },
  props: {
    title: String
  }
}
</script>

<template>
  <div class="modal" @click.self="$emit('close')">
    <div class="modal-content">
      <div class="modal-header">
        <p class="modal-title">
          {{ title }}
        </p>
        <CloseIcon @click="$emit('close')"/>
      </div>
      <slot></slot>
    </div>
  </div>
</template>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}

.modal-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 40px;
  margin-bottom: 30px;
}

.modal-title {
  font-size: 24px;
  color: black;
}

.modal-content {
  border-radius: 10px;
  padding: 24px;
  background-color: white;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  min-width: 600px;
}

.close-icon {
  width: 16px;
  height: 16px;
  cursor: pointer;
}
</style>
