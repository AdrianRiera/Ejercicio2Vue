<script setup>
    import {computed, reactive} from 'vue'
    import Alerta from './Alerta.vue'

    const alerta = reactive ({
        tipo:'',
        mensaje:''
    })

    const emit = defineEmits(['update:nombre','update:propietario', 'update:alta', 'update:sintomas', 'update:email','guardar-paciente'])

    const props= defineProps({
        id: {
            type: [String, null],
            required: true
        },
        nombre : {type: String,
        required:true
        },
        propietario : {type: String,
        required:true
        },
        sintomas : {type: String,
        required:true
        },
        email : {type: String,
        required:true
        },
        alta : {type: String,
        required:true
        },
    })

    const validar = () => {
        if (Object.values(props).includes('')){
            alerta.mensaje = 'Todos los campos son obligatorios'
            alerta.tipo = 'error'
        }
            emit('guardar-paciente')
            alerta.mensaje = 'Guardado con éxito'
            alerta.tipo = 'exito' 
            setTimeout(() => {
                Object.assign(alerta,{
                    tipo:'',
                    mensaje:''
                })},3000)
            }
        
    const editando = computed(() => {
        return props.id 
    })
        
    
</script>

<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>
        

        <Alerta
            v-if="alerta.mensaje"
            :alerta="alerta"
        />

        <form @submit.prevent="validar"
            class="bg-white shadow-md rounded-lg py-10 px-5"
        >

            <div class="mb-5">
                <label
                    for="mascota"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Nombre Mascota   
                </label>
                <input 
                    @input="$emit('update:nombre', $event.target.value)"
                    id="mascota"
                    type="text"
                    placeholder="Nombre de la mascota"
                    class="border-1 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="nombre"
                >

            </div>

            <div class="mb-5">
                <label
                    for="propietario"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Nombre Propietario   
                </label>
                <input
                    @input="$emit('update:propietario', $event.target.value)"
                    id="propietario"
                    type="text"
                    placeholder="Nombre del Propietario"
                    class="border-1 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="propietario"
                >

            </div>
            <div class="mb-5">
                <label
                    for="email"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Email del Propietario   
                </label>
                <input 
                    @input="$emit('update:email', $event.target.value)"
                    id="email"
                    type="email"
                    placeholder="Email del Propietario"
                    class="border-1 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="email"
                >

            </div>
            <div class="mb-5">
                <label
                    for="alta"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Alta  
                </label>
                <input 
                    @input="$emit('update:alta', $event.target.value)"
                    id="alta"
                    type="date"
                    placeholder="Alta"
                    class="border-1 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="alta"
                >

            </div>
            <div class="mb-5">
                <label
                    for="sintomas"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Síntomas  
                </label>
                <textarea 
                    @input="$emit('update:sintomas', $event.target.value)"
                    id="sintomas"
                    placeholder="Describe los síntomas"
                    class="border-1 w-full p-2 mt-2 placeholder-gray-400 rounded-md h-40"
                    :value="sintomas"
                ></textarea>

            </div>
            <input 
                type="submit"
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
                :value="[editando ? 'Actualizar Paciente' : 'Agregar Paciente']"
            />
        </form>
    </div>
</template>

