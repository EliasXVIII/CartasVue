
<template>
  <h2>Cena {{ contador + 1 /* este +1 es para que sume 1 pero el origen de contador no se modifica, sabemos que un array comienza en 0 pero queda feo que empiece el contador para el usuario en 0*/ }} con el rey godo {{ rey }} </h2>

  <h3 class="precio">Precio: {{productos[contador].precio}}€</h3>
  
  <div v-if="productos[contador].finDeSemana" class="todosLosDias dias" >(solo fines de semana)</div>
  <div v-else  class="dias soloFinesDeSemana" >(de lun a dom)</div>
  <br>

  <div v-if="productos[contador].precio<100" class="oferta">
    <div>ahora un 10% de descuento! {{ nuevoPrecio }} € <!-- esto no es una Variable es una propiedad computada -->
    </div>
  <img src="/oferta.jpg" alt="Rey Godo en Descuento"> <!-- voy a poner la ruta completa porque esta en public  -->
  </div>


  <img :src="imagen" alt=""/> <!-- imagen dinámica -->
  <!-- no olvidar colocar el ":src="para colocar la constante computada" -->
  <br>
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

const nuevoPrecio = computed(()=>{
  return Number(productos[contador.value].precio/1.10).toFixed(2) });
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
  border-radius: 0.5rem;
  margin: 5px 0 10px;
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

button{
  margin: 1rem;;
  border: none;
  padding: 1rem;
  width: 25rem;
  font-size: 1rem;
  border-radius: 0.5rem;
}
</style>
