<template>
    <section>
        <h2>Introduzca los productos</h2>
        <form @submit.prevent="submit">
            <label>
                <input v-model="producto.nombre" text placeholder="Nombre"/>
            </label>
              <label>
                <input v-model="producto.precio" number placeholder="precio"/>
            </label>
            <button>Agregar</button>
        </form>

        <ul>
            <li   v-for="producto in listaProductos" :key="producto.nombre">
                <span>{{ producto.nombre }}</span>---------<span>${{ producto.precio }}</span>
            </li>
        </ul>
    </section>
</template>

<script setup lang="ts">
import {  reactive } from 'vue';


type productos = {
 nombre: string
 precio: number
}

let producto: productos = reactive({
    nombre: "",
    precio: 0
})

const listaProductos: Array<productos>  = reactive([])

const submit = () =>{

const nuevoProductos = {
    nombre: producto.nombre,
    precio: producto.precio
}

    listaProductos.push(nuevoProductos)

    Object.assign(producto, {
        nombre: "",
        precio: 0
    });

    console.log(listaProductos)
}




</script>

<style scoped>

ul{
display: flex;
justify-content: center;
border: 1px solid rgb(131, 233, 22);
 width: 400px;

}
li{
    width: 100%;
    display: flex;
    gap: 10px;
    justify-content: space-between;
    padding: 10px;
}
</style>