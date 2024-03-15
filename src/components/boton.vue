<template>
  <button @click="siguiente"> Siguiente ({{ contador + 1 }}/{{total}})</button>
  <button @click="atras"> Atrás ({{ contador }}/{{total}})</button>
</template>

<script setup>

 import {ref, defineEmits} from "vue"
 defineEmits(["siguiente", "atras"]); 

 import { productos } from "../datos.js"; 

 const contador = ref(0);
 

/* const siguiente = ()=>{ 
  contador.value++ ;
 /*  emit("siguiente",contador.value); */
  
 const siguiente = () => { 
  contador.value++; // Incrementa el contador

  // Verifica si el contador ha alcanzado el valor total
  if (contador.value >= productos.length) {
    contador.value = 0; // Reinicia el contador a 0 si es igual o mayor que el total
  }
};
const atras = ()=>{ 
  contador.value--;

  if(contador.value<0){
contador.value=productos.length -1;
  } //si el valor de contador es mayor o igual que la longitud total del []
  
  emit("atras",contador.value);
}; 


</script>

<style scoped>
button{
  margin: 1rem;;
  border: none;
  padding: 1rem;
  width: 25rem;
  font-size: 1rem;
  border-radius: 0.5rem;
}
</style>