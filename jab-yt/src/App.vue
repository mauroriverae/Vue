<script setup>
import { computed, ref } from 'vue';
import { data } from './data';
const count = ref(0);
const color = ref('init');
const modifyCount = (decrement = false) => {
    count.value += decrement ? -1 : 1;
    color.value = count.value < 0 ? "red" : count.value > 0 ? "green" : "";
}
const testVisible = computed(() => { 
    return count.value === 0;
})
const image1 = 'descarga.jpeg';
import image2 from "./assets/logo.svg";
console.log(data[0]['img']);
const image3 = data[0]['img'];
</script>

<template>
    <button @click="modifyCount(true)">-</button>
    <span :class="color">{{ count }}</span>
    <button @click="modifyCount()">+</button>
    <div v-if="count < 0">Write a quantity greater than zero</div>
    <div v-else-if="count>5"> GOOOOOD</div>
    <div v-else>Good quantity</div>
    <div v-show="testVisible">No se permite el nro 0</div>
    <img :src="image3" alt="">
</template>

<style scoped> 
span {
    padding: 5px;
    margin: 10px;
}
.red {
    color: red;
}

.green {
    color:green;
}

.init {
    color: blueviolet;
}
</style>