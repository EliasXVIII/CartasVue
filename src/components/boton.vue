<template>
  <button @click="siguiente"> Siguiente ({{ contador + 1 }}/{{total}})</button>
  <button @click="atras"> Atrás ({{ contador }}/{{total}})</button>
</template>

<script setup>

 import {ref, defineEmits} from "vue"
 defineEmits(["siguiente", "atras"]); 

 const contador = ref(0);
 const total = 10;

const siguiente = ()=>{ 
  contador.value++ ;
  emit("siguiente",contador.value);
  
  if(contador.value>=total) //si el valor de contador es mayor o igual que la longitud total del []
  contador.value=0; //el contador vuelva a su valor 0, en este caso lo expresará como 1 por sumar valor 0del[]+1
//con esta funcion hago que al hacer siguiente vuelva a empezar si el valor del contador supera el total de elementos del Array

};

const atras = ()=>{ 
  contador.value--;

  if(contador.value<o) //si el valor de contador es mayor o igual que la longitud total del []
  contador.value=0;
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