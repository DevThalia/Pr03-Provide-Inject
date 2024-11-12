<script setup>
import { inject, defineProps, defineEmits } from 'vue'

const emit = defineEmits(['anadirProducto'])
const currency = inject('currency')
const props = defineProps({
    productos: {
        type: Array,
        required: true
    }
})

const anadirProducto = (producto) => {
    emit('anadirProducto', producto)
}

const calculoPrecio = (precio) => {
    if (currency.value === 'EURO') {
        return (precio * 0.85).toFixed(2)
    }
    return precio.toFixed(2)
}
</script>

<template>
    <div>
        <h2>Productos</h2>
        <ul>
            <li v-for="(producto, index) in productos" :key="index">
                {{ producto.name }} - {{ calculoPrecio(producto.price) }} {{ currency === 'EURO' ? '€' : '$' }}
                <button @click="anadirProducto(producto)">Añadir</button>
            </li>
        </ul>
    </div>
</template>
