<script>
import ArrowDown from './icons/ArrowDown.vue'

export default {
  name: 'VSelect',
  components: {ArrowDown},
  props: {
    options: Array,
    activeOption: [Object, String]
  },
  data () {
    return {
      selectOpen: false
    }
  },
  methods: {
    selectOption (option) {
      this.selectOpen = false
      this.$emit('select', option)
    }
  }
}
</script>

<template>
  <div class="v-select">
    <div class="v-select-head" :class="{'select-open' : selectOpen}" @click="selectOpen = !selectOpen">
      <p class="v-select-title">{{ activeOption ? activeOption.name : '' }}</p>
      <ArrowDown/>
    </div>
    <div class="v-select-menu" v-show="selectOpen">
      <p class="v-select-item" v-for="option in options" :key="option.id" @click="selectOption(option)">
        {{option.name}}
      </p>
    </div>
  </div>
</template>

<style scoped>
.v-select {
  position: relative;
}

.v-select-head {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 5px 10px;
  border: 1px solid black;
  height: 34px;
  border-radius: 8px;
  width: 400px;
  cursor: pointer;
}

.v-select-title {
  font-size: 16px;
}

.v-select-menu {
  display: flex;
  flex-direction: column;
  border-radius: 8px;
  background-color: white;
  position: absolute;
  left: 0;
  top: 50px;
  width: 100%;
  border: 1px solid black;
  max-height: 300px;
  overflow: scroll;
}

.v-select-item {
  padding: 10px;
  font-size: 16px;
  width: 100%;
  transition: background-color .25s ease;
  cursor: pointer;
  border-radius: 8px;
}

.v-select-item:hover {
  background-color: aliceblue;
}

.select-open {
  .arrow-down {
    transform: rotate(180deg);
  }
}
</style>
