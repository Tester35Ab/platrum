<script>
import TableItem from './TableItem.vue'

export default {
  name: 'UsersTable',
  props: {
    users: Array
  },
  components: {TableItem}
}
</script>

<template>
  <div class="users-table">
    <div class="table-head">
      <p class="table-title" @click="$emit('sort', 'name')">Имя</p>
      <p class="table-title" @click="$emit('sort', 'phone')">Телефон</p>
    </div>
    <table-item v-for="user in users" :key="user.id" :user="user"/>
  </div>
</template>

<style scoped>
.users-table {
  min-width: 50%;
  display: flex;
  flex-direction: column;
}

.table-head {
  display: grid;
  grid-template-columns: 1fr 600px;
}

.table-title {
  padding: 10px;
  font-size: 16px;
  font-weight: 700;
  background-color: aliceblue;
  border: 1px solid black;
  cursor: pointer;
}
</style>
