
<template>
  <div class="container"> 
    <h2>Cena {{ contador + 1 }} con el rey godo {{ rey }} </h2>

    <h3 class="precio">Precio: {{productos[contador].precio}}€</h3>
    
    <div v-if="productos[contador].finDeSemana" class="todosLosDias dias" >(solo fines de semana)</div>
    <div v-else  class="dias soloFinesDeSemana" >(de lun a dom)</div>
    <br>

    <div v-if="productos[contador].precio<100" class="oferta">
      <div class="descuento">ahora un 10% de descuento! {{ nuevoPrecio }} € <!-- esto no es una Variable es una propiedad computada -->
      </div>
      <img src="/oferta.jpg" alt="Rey Godo en Descuento"> <!-- voy a poner la ruta completa porque esta en public  -->
    </div>
    <img :src="imagen" alt=""/> <!-- imagen dinámica -->
    
    <boton /> <!-- no olvidar colocar el ":src="para colocar la constante computada" -->
  </div>
</template>

<script setup>

import {ref, computed } from "vue";
import { productos } from "./datos.js";
import boton from "./components/boton.vue"

const props = defineProps({
  contador: Number,
});
const contador = ref(0);
const ruta = "https://www.html6.es/img/rey_";

const rey = computed(() => {
const elNombre = productos[contador.value].nombre.toLowerCase();
return elNombre.substring(0, 1).toUpperCase() + elNombre.substring(1);
});

const nuevoPrecio = computed(() => {
  return Number(productos[contador.value].precio / 1.10).toFixed(2);
});
</script>
<style scoped>
.container{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.todosLosDias{
  background-color: green;
}

.soloFinesDeSemana{
  background-color: red;
}

.dias{
  color: white;
  padding: 4px 17px;
  font-size: 2rem;
  border-radius: 0.5rem;
  margin: 5px 40px 30px;
  display: inline-block; 
  /* con display Inline Block hago que el ancho se adapte al contenido! */
}
.oferta{
  display: flex;
  align-items: center;
  margin-bottom: 2rem;
}
.oferta img{
  width: 5rem;
  height: auto;
  
}

.descuento{
  font-size: 1.5rem;
}
</style>
