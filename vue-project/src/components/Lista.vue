<template>
    <div>
      <h3>Lista de la Comanda</h3>
      <ul>
        <li v-for="item in cart" :key="item.name">
          {{ item.name }} - ${{ item.price }}
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { inject } from 'vue';
  
  const cart = inject('cart');
  </script>

  