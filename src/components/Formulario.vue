<script setup>
    import { reactive } from 'vue';
    import Alerta from './Alerta.vue';

    const alerta = reactive({
        tipo: '',
        mensaje: ''
    })

    const emit = defineEmits(['update:nombre',
        'update:propietario',
        'update:email',
        'update:alta',
        'update:sintomas',
        'guardar-paciente'
    ])

    const props = defineProps ({
        nombre: {
            type: String,
            required: true
        },
        propietario: {
            type: String,
            required: true
        },
        email: {
            type: String,
            required: true
        },
        alta: {
            type: String,
            required: true
        },
        sintomas: {
            type: String,
            required: true
        }
    })

    const validar = () => {
         if(Object.values(props).includes('')) {
            alerta.mensaje = 'Todos los campos son obligatorios'
            alerta.tipo = 'error'
            return
         }
         //* If the validaion is success emit = save
         emit('guardar-paciente')

         //* Show alert
         alerta.mensaje = 'Guardado Correctamente'
         alerta.tipo = "exito"

         //* Clean the alert
         setTimeout(() => {
            Object.assign(alerta, {
                tipo: '',
                mensaje: ''
            })
         }, 3000);
    }

</script>
<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>
        <p class="text-lg mt-5 text-center mb-10">
            Añade pacientes y
            <span class="text-indigo-600 font-bold">Adminístralos</span>
        </p>

        <Alerta
            v-if="alerta.mensaje"
            :alerta="alerta"
        />
        
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
                        :value="nombre"
                        @input="$emit('update:nombre', $event.target.value)"
                >
            </div>

            <div class="mb-5">
                <label for="propietario" class="block text-gray-700 uppercase font-bold">Nombre del propietario:</label>
                <input type="text" 
                        id="propietario" 
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" 
                        placeholder="Ingresa el nombre del propietario"
                        :value="propietario"
                        @input="$emit('update:propietario', $event.target.value)"
                >
            </div>

            <div class="mb-5">
                <label for="email" class="block text-gray-700 uppercase font-bold">Correo electronico:</label>
                <input type="email" 
                        id="email" 
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" 
                        placeholder="Ingresa un correo electronico"
                        :value="email"
                        @input="$emit('update:email', $event.target.value)"
                >
            </div>

            <div class="mb-5">
                <label for="alta" class="block text-gray-700 uppercase font-bold">Fecha de alta:</label>
                <input type="date" 
                        id="alta" 
                        class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                        :value="alta"
                        @input="$emit('update:alta', $event.target.value)"
                >
            </div>

            <div class="mb-5">
                <label for="sintomas" class="block text-gray-700 uppercase font-bold">Sintomas:</label>
                <textarea id="sintomas" 
                            class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" 
                            placeholder="Ingrese los sintomas"
                            :value="sintomas"
                            @input="$emit('update:sintomas', $event.target.value)"
                ></textarea>
            </div>

            <input type="submit" class="bg-indigo-600 text-white w-full p-3 font-bold uppercase hover:bg-indigo-700 cursor-pointer transition-colors" value="Registrar Paciente">
        </form>
    </div>
</template>
