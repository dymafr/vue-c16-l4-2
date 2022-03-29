<template>
  <div class="p-20">
    <div class="mb-20 d-flex w100 justify-content-center align-items-center">
      <input
        v-model="input"
        @keydown.enter="addItem"
        type="text"
        class="flex-fill mr-20"
      />
      <button class="btn btn-primary mr-20" @click="addItem">Ajouter</button>
    </div>
    <div class="container">
      <TransitionGroup tag="ul">
        <li
          :style="`--i:${index}`"
          class="w-100 card mb-10"
          v-for="(item, index) in items"
          @click="removeItem(index)"
          :key="item"
        >
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
  return Math.floor(Math.random() * this.items.length);
}

function add() {
  this.items.splice(this.randomIndex(), 0, this.nextNum++);
}

function remove() {
  this.items.splice(this.randomIndex(), 1);
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
