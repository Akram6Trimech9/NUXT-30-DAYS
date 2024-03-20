<template>
  <div class="option-container">
    <h4>{{ option.title }}</h4>
    <div class="option-buttons">
      <button
        v-for="(value, index) in option.buttons"
        :key="value"
        class="option"
        :class="{
          active: options[option.category] === value,
          lf: index === 0,
          rt: index === option.buttons.length - 1
        }"
        @click="() => options[option.category] = value"
      >
        {{ value }}
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { Gender, Popularity } from '~/data';
import { Length } from '../data';

interface OptionProps {
  option: {
    title: string;
    category: string;
    buttons: Gender[] | Length[] | Popularity[];
  };
  options: {
    gender: Gender;
    popularity: Popularity;
    length: Length;
  };
}
const props = defineProps<OptionProps>();
</script>

<style scoped>
.option-container {
  margin-bottom: 2rem;
}
.option.active {
  background-color: rgb(249, 87, 89);
  color: white;
  font-weight: bold;
}
.option {
  background-color: white;
  outline: 0.15rem solid rgb(249, 87, 89);
  border: none;
  padding: 0.75rem;
  width: 12rem;
  font-size: 1rem;
  color: rgb(27, 60, 138);
  cursor: pointer;
  font-weight: 200;
}
.lf {
  border-radius: 1rem 0 0 1rem;
}
.rt {
  border-radius: 0 1rem 1rem 0;
}
</style>
