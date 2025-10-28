<script setup>
    import { reactive } from 'vue';
    import Alerta from './Alerta.vue';

    const alerta = reactive({
        tipo: '',
        mensaje: ''
    })

    const paciente = reactive({
        nombre: '',
        propietario: '',
        email: '',
        alta: '',
        sintomas: '',
    })

    const validar = () => {
         if(Object.values(paciente).includes('')) {
            alerta.mensaje = 'Todos los campos son obligatorios'
            alerta.tipo = 'error'
            return
         }          
    }

</script>
<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>
        <p class="text-lg mt-5 text-center mb-10">
            Añade pacientes y
            <span class="text-indigo-600 font-bold">Adminístralos</span>
        </p>
        
        <form action="#" 
                class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
                @submit.prevent="validar"
        >
            <div class="mb-5">
                <label for="mascota" class="block text-gray-700 uppercase font-bold">Nombre de la mascota:</label>
                <input type="text" 
                        id="mascota" 
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" 
                        placeholder="Ingresa el nombre de la mascota"
                        v-model="paciente.nombre"
                >
            </div>

            <div class="mb-5">
                <label for="propietario" class="block text-gray-700 uppercase font-bold">Nombre del propietario:</label>
                <input type="text" 
                        id="propietario" 
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" 
                        placeholder="Ingresa el nombre del propietario"
                        v-model="paciente.propietario"
                >
            </div>

            <div class="mb-5">
                <label for="email" class="block text-gray-700 uppercase font-bold">Correo electronico:</label>
                <input type="email" 
                        id="email" 
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" 
                        placeholder="Ingresa un correo electronico"
                        v-model="paciente.email"
                >
            </div>

            <div class="mb-5">
                <label for="alta" class="block text-gray-700 uppercase font-bold">Fecha de alta:</label>
                <input type="date" 
                        id="alta" 
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                        v-model="paciente.alta"
                >
            </div>

            <div class="mb-5">
                <label for="sintomas" class="block text-gray-700 uppercase font-bold">Sintomas:</label>
                <textarea id="sintomas" 
                            class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" 
                            placeholder="Ingrese los sintomas"
                            v-model="paciente.sintomas"
                ></textarea>
            </div>

            <input type="submit" class="bg-indigo-600 text-white w-full p-3 font-bold uppercase hover:bg-indigo-700 cursor-pointer transition-colors" value="Registrar Paciente">
        </form>
    </div>
</template>
