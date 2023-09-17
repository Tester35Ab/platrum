<template>
  <div id="app">
    <Header @add="showAddModal = true"/>
    <main class="main-page">
      <UsersTable :users="users" @sort="sortUsers"/>
      <transition name="fade">
        <AddModal v-if="showAddModal" @close="showAddModal = false" :users="users" @add="addUser"/>
      </transition>
    </main>
  </div>
</template>

<script>
import VBtn from './components/UI/VBtn.vue'
import Header from './components/Header.vue'
import TableItem from './components/users/TableItem.vue'
import UsersTable from './components/users/UsersTable.vue'

export default {
  name: 'App',
  components: {
    UsersTable,
    TableItem,
    Header,
    VBtn,
    AddModal: () => import('./components/modal/AddModal.vue')
  },
  data () {
    return {
      showAddModal: false,
      users: [],
      sortedUsers: [],
      isSorted: false
    }
  },
  watch: {
    users: {
      handler: function (updatedList) {
        localStorage.setItem('users', JSON.stringify(updatedList))
      },
      deep: true
    }
  },
  methods: {
    addUser ({user, parent}) {
      if (parent) {
        parent.subordinates.push(user)
      } else {
        this.users.push(user)
      }
      this.showAddModal = false
    },
    prepare (value) {
      return value.replace(/[^a-zа-яё0-9\s]/gi, '').replaceAll(' ', '')
    },
    sortSubordinates (user, param) {
      user.subordinates = user.subordinates.sort((a, b) => this.prepare(a[param]).localeCompare(this.prepare(b[param])))
      user.subordinates.forEach(subordinate => this.sortSubordinates(subordinate, param))
    },
    sortUsers (param) {
      const sorted = this.users.sort((a, b) => this.prepare(a[param]).localeCompare(this.prepare(b[param])))
      sorted.forEach(user => this.sortSubordinates(user, param))
      this.sortedUsers = sorted
    },
    getUsers () {
      this.users = JSON.parse(localStorage.getItem('users')) || []
      this.sortedUsers = JSON.parse(JSON.stringify(this.users))
    }
  },
  mounted () {
    this.getUsers()
  }
}
</script>

<style>
#app {
  height: 100%;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.main-page {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
