<script setup>
import { computed, provide, ref, defineEmits } from 'vue'
import MenuList from './menuList.vue'

const titulo = ref('Pedido nuevo')
const pedidoActual = ref([])

const currency = ref('EURO')
provide('currency', currency)

const productos = [
    { name: "Hamburger 🍔", price: 5 },
    { name: "Cheeseburger 🧀", price: 6 },
    { name: "Impossible Burger 🥕", price: 7 },
    { name: "Fries 🍟", price: 2 }
]

const detallePedido = computed(() => {
    return pedidoActual.value.map(producto => `${producto.name} - ${producto.price} ${currency.value}`)
})

const emit = defineEmits(['anadirProducto', 'realizarPedido'])

const realizarPedido = () => {
    if (pedidoActual.value.length === 0) {
        alert('No hay productos en el pedido')
        return
    }

    alert(`Tu pedido "${titulo.value}" ha sido realizado con éxito. Resumen: ${detallePedido.value.join(', ')}`)
    emit('realizarPedido')  // Emite el evento para vaciar la cesta
    pedidoActual.value = []
    titulo.value = 'Pedido nuevo'
}

const editarPedido = (producto) => {
    pedidoActual.value.push(producto)
    emit('anadirProducto', producto)
}
</script>

<template>
    <header>
        <h1>{{ titulo }}</h1>
        <input type="text" v-model="titulo" placeholder="Escribe un nuevo nombre aquí" />

        <button type="submit" @click="realizarPedido">Place Order</button>
    </header>

    <div class="currency-container">
        <p>Moneda</p>
        <select v-model="currency">
            <option value="EURO">Euros (€)</option>
            <option value="USD">Dólares ($)</option>
        </select>
    </div>

    <MenuList @anadirProducto="editarPedido" :productos="productos" />
</template>
