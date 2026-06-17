<script setup>
import {ref} from 'vue'
//const message=ref('Hello Word')

const text= ref(0

)
const count = ref(0)
function increment (){
    count.value++
}
function onInput(e){
    message.value = e.target.value
}
</script>
<template>
    <div id = "center">
        <h1>{{message}}</h1>
        <input type = "text" v-model="message" placeholder="Escibe algo..." />
        <button @click="increment">Contar</button>
        <p> El contador es:
            {{ count }}
        </p>
>        {{counter}}
        </div>
</template>