<template>
  <h2>Cena {{ contador + 1 }}
    con el rey godo {{ rey }}
  </h2>
  <h3 class="precio"> Precio: {{ productos[contador].precio }} $ </h3>
  <div v-if="productos[contador].finDeSemana" class="soloFinesDeSemana dias">Solo Fines de Semana</div>
  <div v-else class=" dias todosLosDias">De lunes a Domingo</div>
  <div v-if="productos[contador].precio<100" class="Oferta">
    <div>Ahora un 10% dto: {{ nuevoPrecio }} $</div>
    <img src="/Oferta.jpg" alt="rey godo en descuento"/>
  </div>
  <img :src="imagen" alt="">
  <button @click="siguiente">Siguiente ({{ contador + 1 }}/ {{total}} )</button>
</template>

<script setup>
  import { ref, computed } from 'vue';
  import {productos} from "./datos";
 

  const contador = ref(0);
  const total = productos.length;
  const ruta= "https://www.html6.es/img/rey_";
  const siguiente = () => {
    contador.value++;
    if (contador.value>=total){
      contador.value=0;
    }
  };
  const rey = computed(()=>{
    const Elnombre =productos[contador.value].nombre.toLowerCase()
    return Elnombre.substring(0,1).toUpperCase() + Elnombre.substring(1)
  })

  const imagen = computed(()=>{
    return `${ruta}${productos[contador.value].nombre.toLowerCase()}.png`

  })

  const nuevoPrecio = computed(()=>{
    return Number(productos[contador.value].precio/1.10).toFixed(2)
  })
</script>

<style scoped>
  .todosLosDias{
    background-color: green;
  }
  .soloFinesDeSemana{
    background-color:red ;
  }
  
</style>
