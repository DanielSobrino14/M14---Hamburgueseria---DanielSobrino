<template>
  <div class="Xat"></div>
  <h1>{{ nombrePedido }}</h1>
  <input v-model="nombrePedido" />
  <button @click="enviarPedido">Enviar Pedido</button>
  <Producte :productes="productes" @añadir-al-carrito="añadirAlCarrito"/>
</template>

<script setup>
import { ref, provide } from 'vue';
import Producte from './components/Productes.vue';
import Lista from './components/Lista.vue'

const nombrePedido = ref("");
const cart = ref([]);

const productes = ref([
  { name: "Hamburger 🍔", price: 5 },
  { name: "Cheeseburger 🧀", price: 6 },
  { name: "Impossible Burger 🥕", price: 7 },
  { name: "Fries 🍟", price: 2 }
]);

provide('cart', cart);

const añadirAlCarrito = (producto) => {
  cart.value.push(producto);
  alert(`Añadido ${producto.name} - $${producto.price} a la comanda.`);
};

</script>
