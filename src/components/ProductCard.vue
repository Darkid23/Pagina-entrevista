<script setup>
defineProps({
    producto: Object
})
</script>
<template>
    <div class="bg-white p-6 rounded-xl shadow-md border-gray-100 hover:shadow-xl transition-shadow duration-300">
        <div class="mb-4">
            <h3 class="text-lg font-bold text-gray-800">{{ producto.name }}</h3>
            <p class="text-sm text-gray-500">Proveedor: {{ producto.proveedor }}</p>
        </div>
    
    <div class="flex justify-between items-center border-t pt-4">
        <span class="text-2xl font-bold text-gray-900">${{ producto.price }}</span>
        <span
            class="px-3 py-1 rounded-full text-xs font-bold border"
            :class="{
                'bg-red-100 text-red-800 border-red-200': producto.stock < 5,
                'bg-green-100 text-green-800 border-green-200': producto.stock >= 5
            }"
            >
            {{ producto.stock <5 ?  'Poco Stock!' : 'Disponible' }}
        </span>
    </div>
</div>
</template>