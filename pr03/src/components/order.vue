<script setup>
import {ref} from 'vue'
let titulo = ref('')

</script>

<template>
    <h1> {{ titulo }}</h1>
    <input type="text" name="titulo" id="titulo" v-model="titulo">
    <button type="submit">Place order</button>
</template>
