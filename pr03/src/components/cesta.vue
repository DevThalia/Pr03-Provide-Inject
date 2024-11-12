<script setup>
import { defineProps } from 'vue'

const props = defineProps({
    cesta: {
        type: Array,
        required: true
    }
})
</script>

<template>
    <div>
        <h2>Cesta de la compra</h2>
        <ul>
            <li v-for="(item, index) in cesta" :key="index">
                {{ item.name }} - {{ item.price }} €
            </li>
        </ul>
    </div>
</template>
