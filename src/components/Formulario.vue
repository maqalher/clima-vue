<script setup>

    import { reactive, ref } from 'vue';
    import Alerta from './Alerta.vue';

    const emit = defineEmits(['obtenerClima'])

    const busqueda = reactive({
        ciudad: '',
        pais: ''
    })

    const error = ref('')

    const paises = [
        { codigo: 'US', nombre: 'Estados Unidos' },
        { codigo: 'MX', nombre: 'México' },
        { codigo: 'AR', nombre: 'Argentina' },
        { codigo: 'CO', nombre: 'Colombia' },
        { codigo: 'CR', nombre: 'Costa Rica' },
        { codigo: 'ES', nombre: 'España' },
        { codigo: 'PE', nombre: 'Perú' }
    ]

    const consultarClima = () => {
        if(Object.values(busqueda).includes('')){
            error.value = 'Todos los campos con obligatorios'
            return
        }
        error.value = ''
        emit('obtenerClima', busqueda)
    }
</script>

<template>
    <form
        class="formulario"
        @submit.prevent="consultarClima"
    >   
        <Alerta v-if="error">{{ error }}</Alerta>
        <div class="campo">
            <label for="ciudad">Ciudad</label>
            <input 
                type="text"
                id="ciudad"
                placeholder="Ciudad"    
                v-model="busqueda.ciudad"
            >
        </div>
        <div class="campo">
            <label for="pais">Pais</label>
            <select 
                id="pais"
                v-model="busqueda.pais"
            >
                <option value="">-- Seleccione un pais</option>
                <option v-for="pais in paises" :key="pais.codigo" :value="pais.codigo">{{ pais.nombre }}</option>
            </select>

            <input type="submit" value="Consultar Clima">
        </div>
    </form>
</template>
