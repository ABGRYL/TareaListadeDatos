<script setup lang="ts">
import type { IProductos } from '@/interface/IProductos';

const productos = defineProps<IProductos>();
</script>

<template>
        <table>
            <td>ID: {{ productos.id }} </td>
            <td>Artículo: {{ productos.artículo }} </td>
            <td>Unidad: {{ productos.unidad }} </td>
            <td>Peso: {{ productos.peso }} </td>
            <td>Precio:  {{ productos.precio }}</td>
        </table>
    
</template>

<style scoped>

th, td {
  border: 1px solid #000000;
  padding: 8px;
}
td {
  padding: 8px;
}

button {
  background-color: #d000ff;
  color: #ffffff;
  border: none;
  padding: 8px 12px;
  cursor: pointer;
}
</style>