<template>
  <div>
    <button @click="siguiente">Siguiente ({{ contador + 1 }}/{{ total }})</button>
    <button @click="atras">Atrás ({{ contador }}/{{ total }})</button>
    <img :src="imagen" alt="">
  </div>
</template>

<script setup>
import { ref, defineEmits, watchEffect } from "vue";
import { productos } from "../datos.js";

defineEmits(["siguiente", "atras"]);

const contador = ref(0);
const total = productos.length;
const ruta = "https://www.html6.es/img/rey_"; // Cambiar la ruta por la ruta correcta

const siguiente = () => {
  contador.value++;
  if (contador.value >= total) {
    contador.value = 0;
  }
};

const atras = () => {
  contador.value--;
  if (contador.value < 0) {
    contador.value = total - 1;
  }
};

const imagen = ref('');


watchEffect(() => {
  imagen.value = `${ruta}${productos[contador.value].nombre.toLowerCase()}.png`;
});

</script>

<style scoped>
button {
  margin: 1rem;
  border: none;
  padding: 1rem;
  width: 25rem;
  font-size: 1rem;
  border-radius: 0.5rem;
}
</style>
