<template>
    <div class="movements">
      <h2 class="title">Historial</h2>
      <div class="content">

        <Movement 
           v-for="{id, title, description, amount} in movements"
           :key="id"
           :id="id"
           :title="title"
           :description="description"
           :amount="amount"
           @remove="remove"
         >
        </Movement>

      </div>
    </div>
</template>
<script setup>
import { toRefs, defineProps, defineEmits} from 'vue'; 
import Movement from "@/components/Movements/Movement.vue"    

const props = defineProps({
   movements: {
    type: Array,
    default: ()=> [],
   }
}) ;

const {movements} = toRefs(props);

const emit = defineEmits(["remove"])

const remove = (id) => {
   emit("remove",id)
}


    


</script>
<style scoped>
.movements {
  max-height: 100%;
  padding: 16px;
  margin-bottom: 20px;
  background-color: #ffffff; /* Fondo blanco para resaltar la sección */
  border-radius: 8px; /* Bordes redondeados para un look más moderno */
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1); /* Sombra sutil para dar profundidad */
}

.title {
  margin: 0 0 24px 0;
  color: var(--brand-blue, #007bff); /* Usa el color de la marca o un fallback */
  font-size: 1.8rem; /* Tamaño de fuente aumentado para más impacto */
  font-weight: bold; /* Título más destacado */
  text-align: center; /* Centra el título */
  border-bottom: 2px solid var(--brand-blue, #007bff); /* Línea decorativa debajo del título */
  padding-bottom: 10px; /* Espacio entre el título y la línea decorativa */
}

.content {
  max-height: 60vh;
  display: flex;
  flex-direction: column;
  gap: 12px; /* Más espacio entre elementos para una separación visual clara */
  overflow-y: auto; /* Ajuste de scroll para contenido largo */
  padding-right: 8px; /* Asegura que el contenido no toque los bordes */
}

/* Estilo para cada movimiento */
.content > div {
  padding: 12px;
  background-color: #f9f9f9; /* Fondo claro para cada elemento */
  border: 1px solid #e0e0e0; /* Borde sutil para separar cada movimiento */
  border-radius: 5px; /* Bordes redondeados para cada ítem */
  font-size: 1rem; /* Ajusta el tamaño de la fuente */
  color: #333; /* Color del texto */
  transition: background-color 0.3s ease; /* Transición suave para el hover */
}

/* Efecto hover para los elementos de movimiento */
.content > div:hover {
  background-color: #f0f0f0; /* Cambio de color de fondo al pasar el cursor */
}
</style>
