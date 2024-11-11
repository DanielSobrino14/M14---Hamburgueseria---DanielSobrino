<template>
  <div>
    <div v-for="producto in productos" :key="producto.name">
      <span>{{ producto.name }} - {{ producto.precioFormateado }}</span>
      <button @click="añadirAlCarrito(producto)">Añadir a la comanda</button>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  productos: Array
});

const emitir = defineEmits(['añadir-al-carrito']);

const añadirAlCarrito = (producto) => {
  emitir('añadir-al-carrito', producto);
};
</script>
<style scoped>
div {
  margin: 10px 0;
}

span {
  font-size: 16px;
  color: #333;
  margin-right: 15px;
}

button {
  background-color: #1e90ff;
  color: white;
  font-size: 14px;
  padding: 5px 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #187bcd;
}

button:active {
  background-color: #125a8e;
}
</style>

