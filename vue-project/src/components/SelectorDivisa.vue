<template>
  <div>
    <label for="divisa">Moneda:</label>
    <select id="divisa" v-model="divisaSeleccionada" @change="emitirDivisa">
      <option value="USD">Dólares ($)</option>
      <option value="EUR">Euros (€)</option>
    </select>
  </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue';

const emitir = defineEmits(['cambio-divisa']);
const divisaSeleccionada = ref('USD');

const emitirDivisa = () => {
  emitir('cambio-divisa', divisaSeleccionada.value);
};
</script>
<style scoped>
div {
  margin: 15px 0;
  text-align: center;
}

label {
  color: #1e90ff;
  font-weight: bold;
  margin-right: 10px;
}

select {
  padding: 5px 10px;
  font-size: 16px;
  color: #1e90ff;
  border: 1px solid #a2c7e5;
  border-radius: 4px;
  background-color: white;
  cursor: pointer;
}

select:focus {
  outline: none;
  border-color: #1e90ff;
}
</style>


