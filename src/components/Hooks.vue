<template>
    <div>
        <h1>{{ msg }}</h1>
        <div ref="container"></div>
        <input type="text" v-model="nombre">
        <input type="text" v-model="apellido">
        <button @click="mostrarDatos"> mostrar datos </button>
        <h2>{{ nombre }} {{ apellido }}</h2>

    </div>
</template>

<script setup lang="ts">
import { onBeforeMount, onBeforeUnmount, onBeforeUpdate, onMounted, onUnmounted, onUpdated, ref } from 'vue'

const nombre = ref("")
const apellido = ref("")
let persona = {}
function mostrarDatos() {
    alert(nombre.value + apellido.value)
    persona = { nombre: nombre.value, apellido: apellido.value }
    console.log(persona)
}
const msg = ref("PWD")
const container = ref()


console.log("componente en setup")

//  --- hooks del ciclo de vida de un componente --- //
onBeforeMount(() => {
    msg.value += " 2025"
    console.log("componente aun no montado")
})
// para peticiones a APIs
onMounted(() => {
    msg.value += " componente montado"
    console.log("componente aun montado")
})
// manejo de estilos
onBeforeUpdate(() => {
    console.log("componente antes de actualizar")
}) // manejo de estilos
onUpdated(() => {
    console.log("componente actualizado")
})
// para limpieza de listeners, reseteo de stores, etc
onBeforeUnmount(() => {
    console.log("componente antes de Desmontarlo")

})
// para limpieza de listeners, 
// limpieza de paquetes externos, envio de logs de componente
onUnmounted(() => {
    console.log("componente Desmontado")
})
</script>

<style scoped></style>