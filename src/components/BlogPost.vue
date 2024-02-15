<script setup>

// Import the defineProps function
defineProps({
    title: String,
    id: Number,
    subtitle: {
        type: String,
        default: 'Without description'
    },
    colorText: String
})

// Import the defineEmits function
const emit = defineEmits(['changeFavoriteName'])

// Import the capitalize function
import { capitalize } from '../utils/functions.js'

</script>

<template>
    <div class="card w-100">
        <div class="card-body">
            <h5 class="card-title" :class="`text-${colorText}`"> {{ (id) }} - {{ capitalize(title) }}</h5>
            <p> {{ subtitle }}</p>
            <button @click="emit('changeFavoriteName', title)" class="btn btn-primary">Favorite</button>
        </div>
    </div>
</template>