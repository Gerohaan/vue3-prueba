<script setup>
import { ref, computed } from "vue"
const name = "Vue dinámico"

const counter = ref(0)

const listAddCount = ref([])

const disableCouter = ref(false)

const increment = () => {
  counter.value ++
}

const decrement = () => {
  counter.value --
}

const reset = () => {
  counter.value = 0
  disableCouter.value = false 
  listAddCount.value = []
}

const classCounter = computed(() => {
  if(counter.value === 0){
    return 'color: blue;'
  }
  if(counter.value > 0){
    return 'color: green;'
  }
  if(counter.value < 0){
    return 'color: red;'
  }
})


const add = () => {
  if(listAddCount.value.length > 0){
    let findCounter = listAddCount.value.find(item => item === counter.value)
    if(findCounter === counter.value){
      disableCouter.value = true
      return false
    }else{
      disableCouter.value = false
      listAddCount.value.push(counter.value)
    }
  }else{
    listAddCount.value.push(counter.value)
  }
}

</script>
<template>
  <h1>Hola {{ name.toUpperCase() }}</h1>
  <h2 :style="classCounter">{{ counter }}</h2>
  <p>
    <button @click="increment()">Aumentar</button>
    <button @click="decrement()">Disminuir</button>
    <button @click="reset()">Reiniciar</button>
    <button :disabled="disableCouter" @click="add()">Add +</button>
  </p>
  <section>
    <ul>
      <li v-for="(list, index) in listAddCount" :key="index">
        {{ list }}
      </li>
    </ul>
  </section>
</template>
<style>
h1{
  color:brown;
}
</style>