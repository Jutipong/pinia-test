<template>
  <h1>Grocery List App Count {{mainStore.ItemCount}}</h1>
  <!-- <h1>Test * 5 = {{test}}</h1> -->

  <button @click="createItem">New Item</button>
  <button @click="reset">New Item</button>

  <div>
    <div
      v-for="(item, index) in mainStore.items"
      :key="index"
      style="background-color: #f5f5f5; padding: 10px; margin-bottom: 10px; margin-top: 10px;"
    >
      <code>{{ item }}</code>
      <button @click="deleteItem(item.id)">Delete</button>
      <button @click="updateItem(item.id)">Update</button>
    </div>
  </div>
</template>

<script  lang="ts" setup>
import { watch, computed } from "vue";
import { generateFakeData } from "./models/item.model";
import { useMainStore } from "./store/index";
const mainStore = useMainStore();

watch(mainStore.items, () => {
  console.log("test watch", mainStore.items);
}
)
function createItem() {
  mainStore.createNewItem(generateFakeData());
}
function deleteItem(id: string) {
  mainStore.deleteItem(id);
}
function updateItem(id: string) {
  mainStore.updateItem(id, generateFakeData());
}
function reset() {
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>