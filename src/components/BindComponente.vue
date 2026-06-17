<script setup>
import {ref} from 'vue'

const titleClass = ref('title')
const message=ref('Hello Word')
</script>

<template>
    <div id = "center">
        <h1 :class="titleClass">{{message}}</h1>
        {{counter}}
        </div>
</template>

<style>
.title {
    color: red;
}
</style>