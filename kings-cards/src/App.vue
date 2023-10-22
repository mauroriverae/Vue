<script setup>
import { ref, computed } from 'vue';
import { productos } from './data.js';

const count = ref(0);
const total = productos.length;

const modify = () => {
    count.value === total - 1 ? count.value = 0 : count.value++;
}
const rey = computed(() => {
    const name = productos[count.value].nombre.toLocaleLowerCase();
    return name.substring(0,1).toUpperCase() + name.substring(1);
})
const imgRey = computed(() => {
    const nameUrl = rey.value.toLocaleLowerCase()
    return `https://www.html6.es/img/rey_${nameUrl}.png`
})

const newPrice = computed(() => {
    return Number(productos[count.value].precio/1.10).toFixed(2);
})
</script>

<template>
    <h2>Cena {{ count + 1 }} Con el rey {{ rey }}</h2>
    <h3 class="precio">Price: ${{ productos[count].precio }}</h3>
    <div v-if="productos[count].finDeSemana" class="everyDays days">Every days</div>
    <div v-else class="onlyWeekends days">Only weekends</div>
    <div v-if="productos[count].precio <100" class="offer">
        <div>10% off: ${{  newPrice }}</div>
        <img src="/oferta.jpg" alt="In offer">
    </div>
    <img :src="imgRey" alt="">
    <button @click="modify" type="button">Siguiente ({{ count + 1 }}/ {{ total }})</button>
</template>

<style scoped>
    .everyDays{
        background-color: green;
    }
    .onlyWeekends {
        background-color: red;
    }
    .days{
        color: white;
        padding: 4px 17px;
        font-size: 0.9em;
        font-weight: bold;
        border-radius: 4px;
        margin: 6px 0px 10px;
        display: inline-block;
    }
    .offer img {
        width: 65px;
        margin: 12px 6px;
    }
</style>