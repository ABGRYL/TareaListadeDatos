<template>
  <div>
    <br>
    <br>
    <h1>Agregar Productos:</h1>
    <form @submit.prevent="agregarNuevoProducto" class="form-style">
      <label for="articulo">Artículo:</label>
      <input id="articulo" v-model="nuevoProducto.artículo" type="text" placeholder="Artículo" required />

      <label for="unidad">Unidad:</label>
      <input id="unidad" v-model="nuevoProducto.unidad" type="number" placeholder="Unidad" required />

      <label for="peso">Peso:</label>
      <input id="peso" v-model="nuevoProducto.peso" type="text" placeholder="Peso" required />

      <label for="precio">Precio:</label>
      <input id="precio" v-model="nuevoProducto.precio" type="number" placeholder="Precio" required />

      <button type="submit" class="Button">Agregar Producto</button>
    </form>
    <br>

<h1>Lista de Productos:</h1>
    <table>
      <tbody>
        <ProductosItems
        v-bind="producto"
        v-for="producto in productosMostrar"
        :key="producto.id"
        @click="seleccionarProducto(producto.id)"
        :producto="producto"
        :class="{ 'selected': producto.id === Sombra }"
        @SayHi="onSayHi" />

      </tbody>
    </table>
      <br>
     </div>
</template>

<script setup lang="ts">
import ProductosData from '../../Data/ProductosData'
import { ref } from 'vue';
import ProductosItems from './ProductosItems.vue';
import type { IProductos } from '@/interface/IProductos';

const nuevoProducto = ref<IProductos>({
  id: 0, 
  artículo: '',
  unidad: 0,
  peso: 0,
  precio: 0
});

const productosMostrar = ref<IProductos[]>([]);
productosMostrar.value = ProductosData;

// Estado para almacenar el ID del producto seleccionado
const Sombra = ref<number | null>(null);

// Función para seleccionar un producto al hacer clic en él
const seleccionarProducto = (id: number) => {
    Sombra.value = id;
};

// Función para encontrar el último ID y establecer el próximo ID automáticamente
const obtenerProximoId = () => {
  const ultimoId = productosMostrar.value.reduce((maxId, producto) => {
    return producto.id > maxId ? producto.id : maxId;
  }, 0);
  return ultimoId + 1;
};

// Función para agregar un nuevo producto
const agregarNuevoProducto = () => {
  const existe = productosMostrar.value.some(producto => (
    producto.artículo === nuevoProducto.value.artículo &&
    producto.unidad === nuevoProducto.value.unidad &&
    producto.peso === nuevoProducto.value.peso &&
    producto.precio === nuevoProducto.value.precio
  ));
  
  if (!existe) {
    // Obtener el próximo ID automáticamente
    const id = obtenerProximoId();
    // Agregar el nuevo producto con el ID generado automáticamente
    productosMostrar.value.push({ ...nuevoProducto.value, id });
    // Limpiar el formulario después de agregar
    nuevoProducto.value = { id: 0, artículo: '', unidad: 0, peso: 0, precio: 0 };
  } else {
    alert('Por favor, complete todos los campos o su producto ya exite en la lista.');
  }
};

const onSayHi = () => {
  console.log('Se ha seleccionado un producto');
};
</script>

<style>
.form-style {
  display: flex;
  flex-direction: column;
  gap: 10px;
  border: 1px solid #000;
  padding: 20px;
  border-radius: 10px;
}

.form-style input {
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #000;
}

.Button {
  padding: 10px;
  border-radius: 5px;
  border: none;
  background-color: rgb(154, 2, 96); 
  color: #fff;
  cursor: pointer;
}

.selected {
  background-color: rgb(201, 117, 177); 
  color: rgb(236, 238, 88); 
}
</style>