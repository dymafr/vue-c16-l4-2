<template>
  <div class="p-20">
    <div class="mb-20 d-flex w100 justify-content-center align-items-center">
      <button class="btn btn-primary mr-20" @click="add">Ajouter</button>
      <button class="btn btn-primary" @click="remove">Enlever</button>
    </div>
    <div class="container">
      <TransitionGroup tag="ul">
        <li class="w-100 card mb-10" v-for="item in items" :key="item">
          {{ item }}
        </li>
      </TransitionGroup>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const nextNum = ref(10);
const items = ref<number[]>([1, 2, 3, 4, 5, 6, 7, 8, 9]);

function randomIndex() {
  return Math.floor(Math.random() * items.length);
}

function add() {
  items.value.splice(randomIndex(), 0, nextNum++);
}

function remove() {
  items.value.splice(randomIndex(), 1);
}
</script>

<style lang="scss">
@import './assets/scss/base.scss';

li {
  cursor: pointer;
}

.list-item {
  display: inline-block;
  margin-right: 10px;
  transition: all 1s;
}

.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

.list-leave-active {
  position: fixed;
}
</style>
