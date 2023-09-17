<script>
import Modal from './Modal.vue'
import VInput from '../UI/VInput.vue'
import VSelect from '../UI/VSelect.vue'
import VBtn from '../UI/VBtn.vue'
export default {
  name: 'AddModal',
  props: {
    users: Array
  },
  components: {
    VBtn,
    VSelect,
    VInput,
    Modal
  },
  data () {
    return {
      name: '',
      phone: '',
      selectedUser: null,
      usersForSelect: []
    }
  },
  methods: {
    prepareUsers (users) {
      users.forEach(user => {
        this.usersForSelect.push(user)
        this.prepareUsers(user.subordinates)
      })
    },
    addUser () {
      this.$emit('add', {
        user: {
          id: Math.floor(Math.random() * (1000 - 1 + 1) + 1),
          name: this.name,
          phone: this.phone,
          subordinates: []
        },
        parent: this.selectedUser
      })
    }
  },
  mounted () {
    this.prepareUsers(this.users)
  }
}
</script>

<template>
  <Modal @close="$emit('close')" title="Добавление пользователя" class="modal">
    <form class="add-modal" @submit.prevent="addUser">
      <div class="input-group">
        <span class="input-title">Имя</span>
        <VInput v-model="name" placeholder="Введите имя" type="text" required/>
      </div>
      <div class="input-group">
        <span class="input-title">Телефон</span>
        <VInput v-model="phone" placeholder="Введите телефон" type="phone" required/>
      </div>
      <div class="input-group" v-if="usersForSelect.length">
        <span class="input-title">Начальник</span>
        <VSelect @select="(user) => selectedUser = user" :options="usersForSelect" :active-option="selectedUser"/>
      </div>

      <VBtn type="submit">
        Сохранить
      </VBtn>
    </form>
  </Modal>
</template>

<style scoped>

.add-modal {
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.input-group {
  display: flex;
  align-items: center;
  gap: 30px;
  justify-content: space-between;
}

.input-title {
  font-size: 18px;
  font-weight: 500;
}
</style>
