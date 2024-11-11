<template>
  <div>
    <h3>Lista de la Comanda</h3>
    <ul>
      <li v-for="item in carrito" :key="item.name">
        {{ item.name }} - {{ formatearPrecio(item.price) }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { inject } from 'vue';

const carrito = inject('carrito');
const divisa = inject('divisa');

const tasasDivisa = {
  USD: 1,
  EUR: 0.85
};

const formatearPrecio = (precio) => {
  const tasa = tasasDivisa[divisa.value];
  const precioConvertido = (precio * tasa).toFixed(2);
  return divisa.value === 'USD' ? `$${precioConvertido}` : `€${precioConvertido}`;
};
</script>

<style scoped>
div {
  background-color: #e6f2fa;
  padding: 15px;
  border-radius: 8px;
  margin-top: 20px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
}

h3 {
  color: #1e90ff;
  font-size: 18px;
  margin-bottom: 10px;
  text-align: center;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

li {
  padding: 8px;
  font-size: 16px;
  color: #333;
  border-bottom: 1px solid #a2c7e5;
}

li:last-child {
  border-bottom: none;
}
</style>


