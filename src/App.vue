<template>
  <!-- Componente principal que muestra la pantalla de carga -->
  <Suspense>
    <template #default>
      <Home/>
    </template>
    <template #fallback>
      <Splashscreen/>
    </template>
  </Suspense>
 
</template>

<script>
// Importa el componente Splashscreen desde la carpeta de componentes
import Splashscreen from "@/components/Splashscreen.vue";
import {  defineAsyncComponent} from "vue";

export default {
  // Registro del componente Splashscreen
  components: {
  Splashscreen,
    Home: defineAsyncComponent(()=>
      new Promise((resolve)=>{
        setTimeout(()=>{
          resolve(import("./components/Home.vue"))


        },2500)
      })
    )
  },
};
</script>

<style>
/* Estilos generales para html, body y la clase .app */
html,
body,
.app {
  min-height: 100vh; /* Asegura que el contenedor ocupe al menos la altura completa de la ventana */
  margin: 0; /* Elimina los márgenes por defecto */
  font-family: Arial, Helvetica, sans-serif; /* Define la fuente predeterminada */
}

/* Variables de color para uso global en el proyecto */
:root {
  --brand-green: #04b500; /* Verde de la marca */
  --brand-blue: #0689b0; /* Azul de la marca */
}

/* Puedes añadir aquí más estilos globales o específicos para tu componente */
</style>
