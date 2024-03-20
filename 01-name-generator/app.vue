<template>
  <div class="container">
    <!-- <NuxtWelcome /> -->
    <h1>Baby Name Generator</h1>
    <p>Choose your options and click on the find Name Button below</p>
    <div class="options-container">
      <Option
        v-for="option in optionsArray"
        :key="option.title"
        :option="option"
        :options="options"
      />

      <button class="primary" @click="computeSelectedNames">FIND NAMES</button>
    </div>
    <div class="card-container">
  <CardName v-for="name in selectedNames" :key="name" :name="name"/>
</div>

  </div>
</template>

<script setup lang="ts">
import {
  Gender,
  Length,
  Popularity,
  names,
  type OptionsState,
  type Name,
} from "./data";

const options = reactive<OptionsState>({
  gender: Gender.GIRL,
  length: Length.SHORT,
  popularity: Popularity.TRENDY,
});
// const closeName = (name:string )=>{
// selectedNames.value=selectedNames.value.filter((item: Name)=> item.name != name)
// }
const selectedNames = ref<string[]>([]);
const computeSelectedNames = () => {
  const filteredNames = names
    .filter((item: Name) => item.gender === options.gender)
    .filter((item: Name) => item.popularity === options.popularity)
    .filter((item: Name) => {
      if (options.length === Length.ALL) return true;
      else return options.length === item.length;
    });

  selectedNames.value = filteredNames.map((item) => item.name);
};

const optionsArray = [
  {
    title: "1) Choose a gender ",
    category: "gender",
    buttons: [Gender.GIRL, Gender.BOY, Gender.UNISEX],
  },
  {
    title: "2) Choose the name's popularity",
    category: "popularity",
    buttons: [Popularity.TRENDY, Popularity.UNIQUE],
  },
  {
    title: "3) Choose name's length ",
    category: "length",
    buttons: [Length.ALL, Length.LONG, Length.SHORT],
  },
];
</script>

<style scoped>

.container {
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}
.container h1 {
  font-size: 3rem;
}
.options-container {
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 0 auto;
  margin-top: 4rem;
  position: relative;
}
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
.primary {
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}
</style>
