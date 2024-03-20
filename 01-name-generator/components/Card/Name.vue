<template>
      <div class="card" >
        <h4>{{ name }}</h4>
        <p>X</p>
      </div>
</template>

<script lang="ts" script>
import {   defineProps } from 'vue';
interface NameProps{
   name :string
}
  const props =defineProps<NameProps>()
</script>
<style scoped>
.card-container {
  display: flex;
  margin-top: 3rem;
  flex-wrap: wrap;
}
.card {
  background-color: rgb(27, 60, 138);
  width: 8%;
  color: white;
  border-radius: 1rem;
  padding: 0.1rem;
  margin-right: 0.5rem;
  position: absolute;
  margin-bottom: 1rem;
}
.card p {
  position: absolute;
  top: -10px;
  right: 5px;
  cursor: pointer;
  color: white;
  font-size: bold;
}
</style>