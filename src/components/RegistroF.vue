<template>
  <section>
    <h2>Introduzca los productos</h2>
    <form @submit.prevent="submit">
      <label>
        <input v-model="producto.nombre" type="text" placeholder="Nombre" />
      </label>
      <label>
        <input v-model="producto.precio" type="decimal" placeholder="precio" />
      </label>
      <button>Agregar</button>
    </form>

    <article>
      <p class="view">
        <span>{{ producto.nombre }}</span> <span>${{ valorItbs }}</span>
        <span>${{ producto.precio }}</span>
      </p>
    </article>

    <table class="tabla-productos">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>ITBS</th>
          <th>Precio</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="producto in listaProductos" :key="producto.nombre">
          <td>{{ producto.nombre }}</td>
          <td>${{ producto.itbs }}</td>
          <td>${{ producto.precio }}</td>
        </tr>
      </tbody>
    </table>

    <div class="total">
      <p>SubTotal: {{ totales.productos }}</p>
      <p>ITBS: {{ totales.itbs }}</p>

      <p>TOTAL: {{ totales.total }}</p>
    </div>
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

let totales = ref({
  itbs: 0,
  productos: 0,
  total: 0,
});

const valorItbs = computed(() => Number((producto.precio * 0.18).toFixed(2)));

const submit = () => {
  const nuevoProductos = {
    nombre: producto.nombre,
    precio: producto.precio,
    itbs: valorItbs.value,
  };

  listaProductos.push(nuevoProductos);
  totales.value.productos = listaProductos.reduce((acc, producto) => {
    return acc + +producto.precio;
  }, 0);

  totales.value.itbs = listaProductos.reduce((acc, producto) => {
    return acc + producto.itbs;
  }, 0);

  totales.value.total = totales.value.itbs + totales.value.productos;

  Object.assign(producto, {
    nombre: "",
    precio: 0,
  });
};
</script>

<style scoped>
article {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* .view {
  width: 300px;
  display: flex;
  gap: 10px;
  background-color: black;
  padding: 20px;
  border-radius: 10px;
  text-align: center;
} */

.tabla-productos {
  width: 500px;
  border-collapse: collapse;
  margin: 20px auto;
  font-family: sans-serif;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.tabla-productos thead {
  background: rgb(131, 233, 22);
  color: #000;
}

.tabla-productos th,
.tabla-productos td {
  padding: 12px 16px;
  text-align: center;
}

.total, .view {
  width: 400px;
  border-collapse: collapse;
  margin: 20px auto;

  border-radius: 12px;
  display: flex;
  justify-content: space-between;
  background-color: black;
  color: azure;
  padding: 10px;

  text-align: center;
  font-size: 1rem;
  font-weight: bold;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
</style>
