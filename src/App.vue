
<template>
 <div class="container"> 
  <h2>Cena {{ contador + 1 /* este +1 es para que sume 1 pero el origen de contador no se modifica, sabemos que un array comienza en 0 pero queda feo que empiece el contador para el usuario en 0*/ }} con el rey godo {{ rey }} </h2>

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
  <!-- no olvidar colocar el ":src="para colocar la constante computada" -->
  <br>
  <boton /> 
 
</div>
</template>



<script setup>


import {ref, computed} from "vue"; //hacer reactivos estos script
import {productos} from "./datos.js" //importar el archivo dato.js para que traiga el array
import boton from "./components/boton.vue"

const contador = ref(0)
const total = productos.length //este length me dara el valor de la longitud de este array 
const ruta = "https://www.html6.es/img/rey_";


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
