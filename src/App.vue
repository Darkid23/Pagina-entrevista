<script setup>
import {ref, computed } from 'vue';
const vistaActual =ref('tabla'); //variable para guardar la vista actual
import ProductCard from './components/ProductCard.vue';
const busqueda =ref(''); //variable para guardar el texto que busque el usuario
const productos =ref([
  {id:1, name:"Computadora Gamer", price:1500, stock:20, proveedor:"DDtech"},
  {id:2, name:"Laptop HP", price:1200, stock:10, proveedor:"HP"},
  {id:3, name:"Mouse inalambrico", price:100, stock:100, proveedor:"Logitech"},
  {id:4, name:"Teclado Mecanico", price:150, stock:90, proveedor:"Blackdragon"},
  {id:5, name:"Silla Gamer", price:500, stock:30, proveedor:"OficinaPro"},
  {id:6, name:"Silla mala", price:300, stock:100, proveedor:"OficinaNoob"},
  {id: 7, name: "Laptop NovaBook X15", price: 18999, stock: 2, proveedor: "TechWorld SA"},
  {id: 8, name: "Monitor 27'' UltraView QHD", price: 5499, stock: 25, proveedor: "VisioTech MX"},
  {id: 9, name: "Teclado Mecánico Kairo RGB", price: 1299, stock: 40, proveedor: "PeriphOne"},
  {id: 10, name: "Mouse Inalámbrico Swift Pro", price: 699, stock: 50, proveedor: "Digital Supplies"},
  {id: 11, name: "PC Gamer TitanX Ryzen 7 + RTX 4060", price: 24999, stock: 6, proveedor: "DDtech"}
])
// computed crea una variable que se recalcula SOLA cuando cambian sus dependencias
const productosFiltrados = computed(() => {
  return productos.value.filter(producto => {
    const termino = busqueda.value.toLocaleLowerCase();
    const coincideNombre = producto.name.toLowerCase().includes(termino);
    return coincideNombre;
  });
});
</script>

<template>
  <div class="bg-gray-100 p-10 min-h-screen">
    <h1 class="text-3xl font-bold mb-5 text-gray-800">Inventario de mi Proyecto</h1>
    <div>
      <button
        @click="vistaActual = 'tabla'"
        class="px-5 py-2 rounded-lg font-bold transittion-colors"
        :class="vistaActual == 'tabla' ? 'bg-blue-600 text-white' : 'bg-gray-200 text-gray-700 hover:bg-gray-300' "
      >
    </button>  
    <button
        @click="vistaActual = 'tarjetas'"
        class="px-5 py-2 rounded-lg font-bold transition-colors"
        :class="vistaActual == 'tarjetas' ? 'bg-blue-600 text-white' : 'bg-gray-200 text-gray-700 hover:bg-gray-300' "
      >
    </button>
    </div>
    <div class="mb-4">
      <input
        v-model="busqueda"
        type="text"
        placeholder="Escribe para buscar un producto..."
        class="p-2 border border-gray-400 rounded-lg w-full maw-w-md shadow-sm focus:ring-2-blue-500 outline-none"
      />
    </div>
    <div v-if="vistaActual === 'tabla'">
    <div class="overflow-hidden rounded-lg shadow-lg border border-gray-200">
      <table class="w-full bg-white text-left border-collapse">
        <thead class="bg-gray-800 text-white">
          <tr>
            <th class="p-3">Nombre</th>
            <th class="p-3">Precio</th>
            <th class="p-3">Stock</th>
            <th class="p-3">Proveedor</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="producto in productosFiltrados" :key="producto.id" class="hover:bg-gray-100 border-b">
            <td class="p-3">{{ producto.name }}</td>
            <td class="p-3 text-green-600 font-bold">${{ producto.price }}</td>
            <td class="p-3">{{ producto.stock }}</td>
            <td class="p-3 text-gray-500">{{ producto.proveedor }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    </div>
      <div v-else>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <ProductCard 
        v-for="item in productosFiltrados" 
        :key="item.id" 
        :producto="item" 
      />
    </div>
    <div v-if="productosFiltrados.length === 0" class="text-center text-gray-500 mt-10">
      <p>No se encontraron productos</p>
    </div>
    </div>
  </div>
</template>