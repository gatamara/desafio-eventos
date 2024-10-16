<template>
    <div class="container">
        <form @submit.prevent>
            <div>
                <label :class="{ 'error': nombre === '', 'valid': nombre !== '' }" for="nombre">Paciente</label>
                <input v-model="nombre" type="text" placeholder="Nombre" />
            </div>
            <div>
                <label :class="{ 'error': fecha === '', 'valid': fecha !== '' }" for="fecha">Fecha</label>
                <input v-model="fecha" type="date" placeholder="fecha" />
            </div>
            <div>
                <label :class="{ 'error': hora === '', 'valid': hora !== '' }" for="hora">Hora</label>
                <input v-model="hora" type="time" />
            </div>
            <div>
                <label :class="{ 'error': gravedad === '', 'valid': gravedad !== '' }" for="gravedad">Gravedad</label>
                <select v-model="gravedad" name="gravedad" id="gravedad">
                    <option value="">Selecciona</option>
                    <option value="baja">Baja</option>
                    <option value="media">Media</option>
                    <option value="alta">Alta</option>
                </select>
            </div>
            <div>
                <label :class="{ 'error': motivo === '', 'valid': motivo !== '' }" for="motivo">Motivo</label>
                <input v-model="motivo" type="text">
            </div>
            <div>
                <button @click.prevent="agregarUsuario">Agregar</button>
            </div>
        </form>

        <div>
            <ul class="card-container">
                <li v-for="(usuario, index) in usuarios" :key="index">
                    <CardUser :nombre="usuario.nombre" :fecha="usuario.fecha" :hora="usuario.hora"
                        :motivo="usuario.motivo" :gravedad="usuario.gravedad" @eliminar="eliminarUsuario(index)" />
                </li>
            </ul>
            <p id="texto" v-if="usuarios.length == 0">Aun no hay consultas registradas</p>
        </div>
    </div>

</template>

<script setup>
import { ref } from 'vue';
import CardUser from './CardUser.vue';

const nombre = ref('');
const fecha = ref('')
const hora = ref('')
const motivo = ref('')
const usuarios = ref([]);
const gravedad = ref('');

const agregarUsuario = () => {

    usuarios.value.push({
        nombre: nombre.value,
        fecha: fecha.value,
        hora: hora.value,
        motivo: motivo.value,
        gravedad: gravedad.value
    });
    limpiarUsuario()
};

const limpiarUsuario = () => {
    nombre.value = '',
        fecha.value = '',
        hora.value = '',
        motivo.value = '',
        gravedad.value = ''
}

const eliminarUsuario = (index) => {
    usuarios.value.splice(index, 1);
};
</script>

<style scoped>
form {
    display: flex;
    gap: 12px;
    justify-content: center;
}

.error {
    color: red;
}

.card-container {
    padding: 24px;
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
}

ul {
    list-style: none;
}

#texto {
    color: crimson;
}
</style>
