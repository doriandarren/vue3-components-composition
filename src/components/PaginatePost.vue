<script setup>

    defineProps(['startPage', 'endPage', 'maxLength']);

    const emit = defineEmits(['next', 'prev']);

</script>


<template>

    <div class="btn-group" role="group" aria-label="Basic example">
        <button 
            @click="emit('prev')" 
            type="button" 
            class="btn btn-outline-primary"
            :disabled="startPage <= 0"
        >
            Previus {{ startPage }}
        </button>

        <button 
            @click="emit('next')" 
            type="button" 
            class="btn btn-outline-primary"
            :disabled="endPage >= maxLength"
        >
            Next {{ endPage}}
        </button>
    </div>

</template>


<style>

</style>