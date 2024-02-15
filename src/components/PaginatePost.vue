<script setup>

defineProps({
    start: Number,
    end: Number,
    maxLength: Number
})

const emit = defineEmits(['next', 'prev'])

const activateNext = () => {
    console.log('Next')
    emit('next')
}

</script>

<template>
    <div class="d-flex flex-column align-items-center">
        <div class="btn-group mb-3" role="group" aria-label="Basic example">
            <button 
                @click="emit('prev')" 
                type="button" 
                class="btn btn-outline-primary"
                :disabled="start <= 0"
            >
                Prev
            </button>
            <button 
                @click="emit('next')" 
                type="button" 
                class="btn btn-outline-primary"
                :disabled="end >= maxLength"
            >
                Next
            </button>
        </div>
        <div>
            <p class="text-primary">{{ start }} - {{ end }}</p>
        </div>
    </div>
</template>