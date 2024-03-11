
<template>
  <h2>Cena {{ contador + 1 /* este +1 es para que sume 1 pero el origen de contador no se modifa */ }} con el rey godo {{ rey }} </h2>

  <h3 class="precio">Precio: {{productos[contador].precio}}€</h3>
  
  <div v-if="productos[contador].finDeSemana" class="todosLosDias dias" >(solo fines de semana)</div>
  <div v-else  class="dias soloFinesDeSemana" >(de lun a dom)</div>
  
  <img :src="imagen" alt=""/> 
  <!-- no olvidar colocar el ":src="para colocar la constante computada" -->
  
  <button @:click="siguiente"> Siguiente ({{ contador + 1 }}/{{total}})</button>
</template>

<script setup>
import {ref, computed} from "vue"; //hacer reactivos estos script

import {productos} from "./datos.js" //importar el archivo dato.js para que traiga el array

const contador = ref(0)
const total = productos.length //este length me dara el valor de la longitud de este array 
const ruta = "https://www.html6.es/img/rey_";

const siguiente = ()=>{ 
  contador.value++ 

  if(contador.value>=total) //si el valor de contador es mayor o igual que la longitud total del []
  contador.value=0; //el contador vuelva a su valor 0, en este caso lo expresará como 1 por sumar valor 0del[]+1
//con esta funcion hago que al hacer siguiente vuelva a empezar si el valor del contador supera el total de elementos del Array

};

const rey = computed (()=>{ //esto es una propiedad computada, se utiliza COMPUTED
  const elNombre=productos[contador.value].nombre.toLowerCase();  //atento a contador.value
  return  elNombre.substring(0,1).toUpperCase() + elNombre.substring(1);//siempre tiene que tener un "return" en computed
})

//imagen sera otra propiedad computada
const imagen = computed(()=>{
    return `${ruta}${productos[contador.value].nombre.toLowerCase()}.png`;
});

</script>


<style scoped>
.todosLosDias{
  background-color: green;
}

.soloFinesDeSemana{
  background-color: red;
}

.dias{
  color: white;
  padding: 4px 17px;
  font-size: 1rem;
  margin: 5px 0 10px;
  display: inline-block; /* con display Inline Block hago que el ancho se adapte al contenido! */
}
</style>
