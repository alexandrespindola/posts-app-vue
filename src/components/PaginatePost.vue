<script setup>

const emit = defineEmits(['next', 'prev'])

</script>

<template>
    <div class="d-flex justify-content-center">
        <div class="btn-group mb-3" role="group" aria-label="Basic example">
            <button @click="emit('prev')" type="button" class="btn btn-outline-primary">Prev</button>
            <button @click="emit('next')" type="button" class="btn btn-outline-primary">Next</button>
        </div>
    </div>
</template>