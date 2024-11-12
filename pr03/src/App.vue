<script setup>
import Order from './components/order.vue'
import Cesta from './components/cesta.vue'
import { ref } from 'vue'

const cesta = ref([])

const agregarACesta = (producto) => {
  cesta.value.push(producto)
}

const vaciarCesta = () => {
  cesta.value = []
}
</script>

<template>
  <div>
    <Order @anadirProducto="agregarACesta"  @realizarPedido="vaciarCesta"/>

    <Cesta :cesta="cesta" />
  </div>
</template>
