<template>
  <section>
    <h2>Introduzca los productos</h2>
    <form @submit.prevent="submit">
      <label>
        <input v-model="producto.nombre" text placeholder="Nombre" />
      </label>
      <label>
        <input v-model="producto.precio" number placeholder="precio" />
      </label>
      <button>Agregar</button>
    </form>

    <article>
      <p class="view">
        <span>{{ producto.nombre }}</span> <span>${{ valorItbs }}</span>
        <span>${{ producto.precio }}</span>
      </p>
    </article>

    <ul>
      <li v-for="producto in listaProductos" :key="producto.nombre">
        <span>{{ producto.nombre }}</span
        >--------- <span>${{ producto.itbs }}</span
        >---------
        <span>${{ producto.precio }}</span>
      </li>
    </ul>
  </section>
</template>

<script setup lang="ts">
import { computed, reactive } from "vue";

type productos = {
  nombre: string;
  precio: number;
  itbs: number;
};

let producto: productos = reactive({
  nombre: "",
  precio: 0,
  itbs: 0,
});

const listaProductos: Array<productos> = reactive([]);



// const valorItbs = computed( () => producto.precio * 0.18)

const valorItbs = computed( () => Math.round(producto.precio * 0.18) )


const submit = () => {

    console.log(valorItbs)

  const nuevoProductos = {
    nombre: producto.nombre,
    precio: producto.precio,
    itbs: valorItbs.value
  };

  listaProductos.push(nuevoProductos)

  Object.assign(producto, {
    nombre: "",
    precio: 0,
  });

  console.log(listaProductos);
};
</script>

<style scoped>

article{
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

.view{
    width: 150px;
    display: flex;
    gap: 10px;
    background-color: black;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
}
ul {
  display: flex;
  justify-content: center;
  border: 1px solid rgb(131, 233, 22);
  width: 400px;
}
li {
  width: 100%;
  display: flex;
  gap: 10px;
  justify-content: space-between;
  padding: 10px;
}
</style>
