<template>
    <div>
      <div v-for="producte in productes" :key="producte.name">
        <span>{{ producte.name }} - ${{ producte.price }}</span>
        <button @click="añadirAlCarrito(producte)">Añadir a la comanda</button>
      </div>
    </div>
  </template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  productes: Array
});

const emit = defineEmits(['añadir-al-carrito']);

const añadirAlCarrito = (producto) => {
  emit('añadir-al-carrito', producto);
};
</script>
