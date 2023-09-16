<script>
import ArrowDown from '../UI/icons/ArrowDown.vue'

export default {
  name: 'TableItem',
  components: {ArrowDown},
  props: {
    user: Object
  },
  data () {
    return {
      rowOpened: false
    }
  },
  methods: {
    openRow () {
      if (this.user.subusers.length) {
        this.rowOpened = !this.rowOpened
      }
    }
  }
}
</script>

<template>
  <div class="table-box">
    <div class="table-item item" :class="{'openable': user.subusers.length, 'open': rowOpened}">
      <div class="name" @click="openRow">
        <ArrowDown v-if="user.subusers.length"/>
        <p>{{ user.name }}</p>
      </div>
      <div class="phone">
        <p>{{ user.phone }}</p>
      </div>
    </div>
    <table-item v-for="subuser in user.subusers" :key="subuser.id" :user="subuser" v-if="rowOpened" class="children"/>
  </div>
</template>

<style scoped>
.table-item {
  display: grid;
  grid-template-columns: 1fr 600px;
}

.item {
  width: 100%;
}

.name {
  display: flex;
  align-items: center;
  gap: 20px;
  border: 1px solid black;
  padding: 10px;
}

.phone {
  padding: 10px;
  border: 1px solid black;
}

.openable {
  cursor: pointer;
  transition: background-color .25s ease;
}

.openable:hover {
  background-color: aliceblue;
}

.open {
  background-color: beige;
  .arrow-down {
    transform: rotate(180deg);
  }
}

.children {
  width: calc( 100% - 5px);
  margin-left: auto;
}
</style>
