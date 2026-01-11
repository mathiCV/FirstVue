<script setup>
  import {ref, computed} from 'vue';
  const name = "vue dinamico";
  const setColor = "color: red;"
  const counter = ref(0);
  const increment = () => {
    console.log("increment +1");
    counter.value++;
    console.log(counter.value);
  }
  const decrease = () => {
    console.log("decrease -1");
    counter.value--;
    console.log(counter.value);
  }

  const classComputer = computed(() => {
    if (counter.value === 0){
      return 'zero'
    }
    if (counter.value > 0){
      return 'positive'
    }
    return 'negative'
  });
  const neutral = () => {
    console.log("reset to 0");
    counter.value = 0;
    console.log(counter.value);
  }
  
  const arrayCounter = ref([]);
  const addNumber = () => {
    arrayCounter.value.push(counter.value);
    console.log(arrayCounter.value);
  }
  const verificar = computed(()=>{
    if (arrayCounter.value.includes(counter.value)){
      return true;
    }
    return false;
  })

</script>

<template>
  <h2 style="display: flex; justify-content: center; margin: 40px auto;" :style="setColor">Buen Vue, {{ name }}</h2>
  <div class="container text-center mt-5">
    <h2 :class="classComputer">{{ counter }}</h2>
    <div class="btn-group">
      <button v-on:click="increment()" class="btn btn-success" >Aumentar</button>
      <button @click="decrease()" class="btn btn-danger" >Disminuir</button>
      <button @click="neutral()" class="btn btn-secondary" >Reset</button>
      <button @click="addNumber()" :disabled="verificar" class="btn btn-primary">Add Number</button>
    </div>  
    <ul class="list-group">
      <li class="list-group-item" v-for="(value, index) in arrayCounter " :key="index">
        {{value}}
      </li>
    </ul>
  </div>
</template>

<style>
  h1{
    color : red;
  }
  
  .positive {
    color : green
  }
  .negative{
    color : red
  }
  .zero{
    color : peru
  }

</style>
