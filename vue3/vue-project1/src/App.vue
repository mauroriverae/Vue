<script setup>
import {ref, computed} from 'vue';
const name = 'dinamic vue';
const styleColor = "color: blue";
const arrColor = ["blue", "red", "black"];
const active = true;
const arrFruits = ["m", "b", "f", "s", "c"];
const arrFruitsSecond = [
    {
        name: "manzana", 
        price: "1000",
        stock: 5,
        description: "one apple"
    },
    {
        name: "pera",
        price: "20",
        stock: 10,
        description: "one pine"
    },
    {
        name: "orange",
        price: "20",
        description: "one orange",
        stock: 20
    }
];

const objFruit =
    {
        name: "pera",
        price: "20",
        description: "one pine"
    }
;
// event methods
const handleClick = (message) => {
    console.log(message);
}
// reactivity
const count = ref(0);

const modifyCount = (decrement = false) => {
    if(decrement) {
        count.value --;
    } else {
        count.value ++;
    }
}
const reset = () => (count.value = 0);

const add = () => {
    favorite.value.push(count.value);
}

const classCounter = computed(() => { 
    if(count.value === 0) {
        return 'zero';
    }  else if (count.value > 0) {
        return 'positive';
    } else {
        return 'negativa';
    }
})

const favorite = ref([]);

const blockAdd = computed(() => {
    const findFavorite = favorite.value.find(num => num === count.value);
    return findFavorite || findFavorite === 0;
})
</script>

<template>
    <div class="cointainer text-center mt-3">
        <div class="baby-steps">
            <h1>Hola {{ name.toUpperCase() }}</h1>
            <h2 :style="styleColor">SFC(Single file component)</h2>
            <h4>{{ active ? "Ready :)" : "Not ready :(" }}</h4>
            <p v-if="!active">Not ready for programming</p>
            <p v-if="active">Ready for programming</p>
            <p v-else-if="active === false">Inactive</p>
            <p v-else>dificult ask</p>
        </div>
        <div class="">
            <h2>v for clasic</h2>
            <ul class="list-group m-3">
                <li class="list-group-item" v-for="(fruits, index) in arrFruits" :key="index">{{ index }} - {{ fruits }}</li>
            </ul>
        </div>
        <div>
            <h2>v-for of objetcs arrays</h2>
            <ul class="list-group m-3">
                <li class="list-group-item" v-for="fruit in arrFruitsSecond" :key="fruit.name">
                    {{ fruit.name }} - {{ fruit.description }} - {{ fruit.price }}
                </li>
            </ul>
        </div>
        <div>
            <h2>v-for objects</h2>
            <ul class="list-group m-3">
                <li class="list-group-item" v-for="(value, property, index) in objFruit" :key="index"> {{ property }} : {{ value }} - {{ index }}</li>
            </ul>
        </div>
        <div>
            <h2>v-for and v-if</h2>
            <ul class="list-group m-3">
                <template v-for="item in arrFruitsSecond" :key="item.name">
                    <li class="list-group-item" v-if="item.stock > 5">
                        {{ item.name }} - {{ item.price }}
                    </li>
                </template>
            </ul>
        </div>
        <div class="boy-steps">
            <h2>Events</h2>
            <div class="btn-group">
                <button class="btn btn-primary" v-on:click="handleClick('H1, how are you?')">Event</button>
                <button class="btn btn-primary" v-on:click="handleClick('soo far soo good men')">Event</button>
            </div>
        </div>
        <div class="click">
            <div class="btn-group mt-3">
                <button class="btn btn-primary" @click.right.prevent="handleClick('right')">right</button>
                <button class="btn btn-primary" @click.middle="handleClick('middle')">middle</button>
                <button class="btn btn-primary" @click.left="handleClick('left')">left</button>
            </div>
        </div>
        <div class="cont">
            <h2 :class="classCounter">{{ count }}</h2>
            <div class="btn-group m-3">
                <button type="button" class="btn btn-success" @click="modifyCount()">+</button>
                <button type="button" class="btn btn-danger" @click="modifyCount('decrement')">-</button>
                <button type="button" class="btn btn-secondary" @click="reset">Reset</button>
                <button type="button" class="btn btn-primary" @click="add" :disabled="blockAdd">Add</button> <br/>
            </div>

            <div>
                <ul class="list-group">
                    <li class="list-group-item mt-3" v-for="(num, index) in favorite">
                        {{ index }}-{{ num }}
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<style>
    h1, h2 {
        color: red;
    }

    .positive {
        color: green;
    }
    .negative {
        color: red;
    }
    .zero {
        color: white;
    }
</style>