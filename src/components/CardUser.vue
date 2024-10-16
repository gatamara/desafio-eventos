<template>
    <div id="card" :class="['card', gravedadClass]">
        <h3>Nombre:</h3>
        <p>{{ nombre }}</p>
        <h3>Fecha:</h3>
        <p>{{ fecha }}</p>
        <h3>Hora:</h3>
        <p> {{ hora }}</p>
        <h3>Motivo: </h3>
        <p>{{ motivo }}</p>

        <button @click="$emit('eliminar')">Eliminar</button>
    </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
    nombre: {
        type: String,
        required: true
    },
    fecha: {
        type: String,
        required: true
    },
    hora: {
        type: String,
        required: true
    },
    motivo: {
        type: String,
        required: true
    },
    gravedad: {
        type: String,
        required: true
    }
});
const gravedadClass = computed(() => {
    if (props.gravedad === 'alta') return 'alta';
    if (props.gravedad === 'media') return 'media';
    if (props.gravedad === 'baja') return 'baja';
    return '';
});
</script>

<style scoped>
#card {
    margin-bottom: 1rem;
    padding: 12px;
    border-radius: 5px;
    width: 300px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 12px;
}

h3,
p {
    font-size: 1rem;
}

h3 {
    font-weight: 600;
}

.alta {
    background-color: red;
}

.media {
    background-color: yellow;
}

.baja {
    background-color: greenyellow;
    color: black;
}
</style>
