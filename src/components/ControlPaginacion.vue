
<template>
    <div>
        <div class="btn-group" role="group" aria-label="Basic outlined example">
        <button 
            @click="emit('previo')" 
            class="btn btn-outline-primary"
            :disabled = "actual <= 1"
        >Anterior</button>
        <button 
            @click="emit('siguiente')" 
            class="btn btn-outline-primary"
            :disabled = "actual >= fin "
        >Siguiente</button>
        </div>
    </div>
</template>

<script setup>
    defineProps(["actual", "fin"]);
    const emit = defineEmits(["siguiente", "previo"]);
</script>

<style lang="scss" scoped>

</style>