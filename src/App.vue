<template>
  <div style="padding: 50px">
    <virtual-list
      v-model="list"
      data-key="id"
      handle=".handle"
      chosen-class="chosen"
      class="virtual-list"
    >
      <template v-slot:item="{ record, index, dateKey }">
        <div class="list-item">
          <div class="item-title">
            <span class="index">#{{ index }}</span>
            <span class="handle">☰</span>
          </div>
          <p>{{ record.desc }}</p>
        </div>
      </template>
    </virtual-list>
    <div>
      <button @click="show2" style="margin-right: 20px">button1: show 2 items</button>
      <button @click="show5" style="margin-right: 20px">button2: show 5 items</button>
      <button @click="show50">button 3: show 50 items</button>
    </div>
    <h3>How to reproduce the error?</h3>
    <ul>
      <li>1. click button1</li>
      <li>2. click button2</li>
      <li>3. click button3</li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import VirtualList from 'vue-virtual-draglist'

const getPageData = (size, from) => {
  const start = from
  // const end = start + size
  return Array.from({ length: size }, (_, i) => {
    const id = start + i
    return {
      id,
      name: `name ${id}`,
      desc: `desc ${id}`,
    }
  })
}
const list = ref(getPageData(50, 0))
const show2 = () => {
  list.value = getPageData(2, 0)
}
const show5 = () => {
  list.value = getPageData(5, 0)
}
const show50 = () => {
  list.value = getPageData(50, 0)
}
</script>

<style scoped>
.virtual-list {
  height: 1000px;
  padding: 0 5px;
  border: 1px solid blue;
}

.list-item {
  position: relative;
  border-radius: 5px;
  box-shadow: 0px 2px 10px -5px #57bbb4;
  padding: 16px;
}

.item-title {
  display: flex;
  justify-content: space-between;
}

.index {
  float: left;
}

.handle {
  cursor: grab;
  text-align: right;
}

.chosen {
  box-shadow: 0px 0px 0px 2px #306aa4;
}
</style>
