<template>
  <section>
    <h2>Introduzca los productos</h2>
    <form @submit.prevent="submit">
      <label>
        <input v-model="producto.nombre" type="text" placeholder="Nombre" />
      </label>
      <label>
        <input v-model="producto.precio" type="number" placeholder="precio" />
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

    <p>{{ totalProducto }}</p>
  </section>
</template>

<script setup lang="ts">
import { computed, reactive, ref } from "vue";

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

let totalProducto = ref(0);

const valorItbs = computed(() => Number((producto.precio * 0.18).toFixed(2)));

const submit = () => {
  const nuevoProductos = {
    nombre: producto.nombre,
    precio: producto.precio,
    itbs: valorItbs.value,
  };

  listaProductos.push(nuevoProductos);
  console.log(typeof listaProductos[0]?.precio)
  totalProducto.value = listaProductos.reduce((acc, producto) => {
    return acc + producto.precio;
  }, 0);

  Object.assign(producto, {
    nombre: "",
    precio: 0,
  });

  console.log(listaProductos);
  console.log(totalProducto.value);
};
</script>

<style scoped>
article {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.view {
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
  flex-direction: column;
  justify-content: center;
  border: 1px solid rgb(131, 233, 22);
  width: 500px;
}
li {
  width: 80%;
  display: flex;
  gap: 10px;
  justify-content: space-between;
  padding: 20px;
}
</style>
