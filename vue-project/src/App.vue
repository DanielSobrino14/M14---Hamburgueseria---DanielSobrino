<template>
  <div class="Xat">
    <h1>{{ nombrePedido }}</h1>
    <input v-model="nombrePedido" placeholder="Nombre del Pedido" />
    <button @click="mostrarLista">Enviar Pedido</button>
    <SelectorDivisa @cambio-divisa="actualizarDivisa" />
    <Productos :productos="productosFormateados" @añadir-al-carrito="añadirAlCarrito" />
    <Lista />
  </div>
</template>

<script setup>
import { ref, provide, computed } from 'vue';
import Productos from './components/Productos.vue';
import Lista from './components/Lista.vue';
import SelectorDivisa from './components/SelectorDivisa.vue';

const nombrePedido = ref("");
const carrito = ref([]);
const divisa = ref('USD');
const productos = ref([
  { name: "Hamburguesa 🍔", price: 5 },
  { name: "Cheeseburger 🧀", price: 6 },
  { name: "Hamburguesa Vegetariana 🥕", price: 7 },
  { name: "Papas Fritas 🍟", price: 2 }
]);


const tasasDivisa = {
  USD: 1,      
  EUR: 0.85    
};

provide('carrito', carrito);
provide('divisa', divisa);

const productosFormateados = computed(() => {
  return productos.value.map(producto => ({
    ...producto,
    precioFormateado: formatearPrecio(producto.price)
  }));
});

const formatearPrecio = (precio) => {
  const tasa = tasasDivisa[divisa.value];
  const precioConvertido = (precio * tasa).toFixed(2);
  return divisa.value === 'USD' ? `$${precioConvertido}` : `€${precioConvertido}`;
};

const actualizarDivisa = (nuevaDivisa) => {
  divisa.value = nuevaDivisa;
};

const añadirAlCarrito = (producto) => {
  carrito.value.push(producto);
  alert(`Añadido ${producto.name} - ${formatearPrecio(producto.price)} a la comanda.`);
};

const mostrarLista = () => {
  if (carrito.value.length > 0) {
    alert(`Comanda Pedida: ${carrito.value.map(item => item.name).join(', ')}`);
    carrito.value = [];
  } else {
    alert('Tu comanda está vacía!');
  }
};
</script>

<style scoped>
.Xat {
  font-family: Arial, sans-serif;
  background-color: #f0f8ff;
  padding: 20px;
  border-radius: 8px;
  max-width: 500px;
  margin: 20px auto;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
}

h1 {
  color: #1e90ff;
  font-size: 24px;
  text-align: center;
  margin-bottom: 20px;
}

input {
  width: calc(100% - 20px);
  padding: 10px;
  font-size: 16px;
  border: 1px solid #a2c7e5;
  border-radius: 4px;
  margin-bottom: 20px;
}

button {
  display: block;
  width: 100%;
  background-color: #1e90ff;
  color: white;
  font-size: 16px;
  font-weight: bold;
  padding: 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 10px;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #187bcd;
}
</style>


