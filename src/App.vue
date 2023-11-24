<script setup>
import { ref, computed } from 'vue'

const name = "vue dinamico";

let counter = ref(0);
const arrayFavs = ref([])

const increment = () => {
  counter.value++
};
const decrement = () => {
  counter.value--
};
const reset = () => {
  (counter.value = 0)
};

const add = () => {
  arrayFavs.value.push(counter.value)
}


// FUNCION CAMBIAR COLOR CON COMPUTED

const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'zero'
  }
  if (counter.value > 0) {
    return 'positive'
  }
  if (counter.value < 0) {
    return 'negative'
  }
});


const repeat = computed(() => {
  const numSearch = arrayFavs.value.find(num => num === counter.value)
  // if (numSearch === 0) return true;
  // return numSearch ? true : false;
  return numSearch || numSearch === 0
})


</script>

<template>
  <div class="container">
    <h1>Hola {{ name.toUpperCase() }}</h1>

    <h2 :class="classCounter">{{ counter }}</h2>

    <button @click="decrement" class="btn down">Disminuir</button>
    <button @click="increment" class="btn up">Aumentar</button>
    <button @click="reset" class="btn reset">Resetear</button>
    <button :disabled="repeat" @click="add" class="btn add">Add</button>
    <ul class="lista">
      <li class="lista ind" v-for="(favs, index) in arrayFavs" :key="index">{{ favs }}</li>
    </ul>
  </div>
</template>

<style>

.lista {
  list-style: none;
  margin-top: 5px;
  margin-left: 150px;
  margin-right: 150px;
}

.lista .ind {
  border: 1px solid black;
}

.container {
  text-align: center;
  margin-top: 10px;
}

h1 {
  color: red;
}

.positive {
  color: green;
}

.negative {
  color: red;
}

.zero {
  color: peru;
}

.btn {
  border-radius: 5px;
  display: inline-block;
  margin: 2px;
  cursor: pointer;
  width: 70px;
  height: 70px;
  border: none;
}

.down {
  background-color: red;
  color: #fff;
}

.up {
  background-color: green;
  color: #fff;
}

.reset {
  background-color: black;
  color: #fff;
}

.add {
  background-color: grey;
  color: #fff;
}
</style>