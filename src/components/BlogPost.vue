<script setup>

    //const props = defineProps(["title", "id", "body", "colorText"])
    //console.log(props)

    defineProps({
        title: String,
        id: Number,
        body: {
            type: String,
            default: 'Sin description'
        }
    })


    const emit = defineEmits(['changeFavourite'])

    

</script>


<template>

    <div class="card">

        <div class="card-body">

            <h5 
                class="card-title"
            >{{id}}-{{title}}</h5>
            <p>{{body}}</p>
            <button 
                @click="emit('changeFavourite', title)" 
                class="btn btn-outline-primary"
                >
                Favorito
            </button>

        </div>

    </div>

</template>


<style>

</style>