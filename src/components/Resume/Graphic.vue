<template>
  <div class="chart-container">
    <!-- Evento que se activa al dejar de tocar la pantalla -->
    <!-- Evento que se activa al tocar la pantalla -->
    <!-- Evento que se activa al mover el dedo en la pantalla -->
    <svg viewBox="0 0 300 200" 
     class="chart"
     @touchstart="tap"      
     @touchmove="tap"       
     @touchend="untap">     
      
      <!-- Línea base que representa el valor cero en el gráfico -->
      <line
        class="base-line"
        :y1="zero"
        :y2="zero"
        x1="0"
        x2="300"
      />

      <!-- Polilínea que representa los datos -->
      <polyline 
        class="data-line"
        :points="points"
      />

      <!-- Línea vertical que aparece durante la interacción táctil -->
      
       <!-- Mostrar solo cuando `showPointer` es true --><line
        v-show¬="showPointer"
        class="vertical-line"
        :x1="pointer"
        y1="0"
        :x2="pointer"
        y2="200"
      />
    </svg>
    <p class="chart-caption">Últimos 30 días</p>
  </div>
</template>

<script setup>
import { defineProps, toRefs, computed, ref, watch,defineEmits } from 'vue';

// Definir las props recibidas por el componente
const props = defineProps({
  amounts: {
    type: Array,          // La prop `amounts` debe ser un array
    default: () => [],    // Valor predeterminado en caso de que no se pase ninguna prop
  },
});

// Desestructurar las props para obtener la referencia `amounts`
const { amounts } = toRefs(props);

// Función para convertir un valor de `amounts` a una posición en píxeles dentro del gráfico
const amountToPixels = (amount) => {
  if (amounts.value.length === 0) return 100; // Valor predeterminado si `amounts` está vacío

  const min = Math.min(...amounts.value);     // Obtener el valor mínimo de `amounts`
  const max = Math.max(...amounts.value);     // Obtener el valor máximo de `amounts`
  const amountAbs = amount + Math.abs(min);   // Ajustar el valor para trabajar con números positivos
  const minMaxRange = Math.abs(max) + Math.abs(min); // Rango total de los datos
  
  // Calcular la posición en el SVG, donde 200 es la altura total
  return 200 - ((amountAbs * 200) / minMaxRange);
};

// Computed property para calcular la posición de la línea base (valor cero)
const zero = computed(() => amountToPixels(0));

// Computed property para generar los puntos de la polilínea en base a los datos
const points = computed(() => {
  const total = amounts.value.length; // Número total de datos
  if (total === 0) return "0,100";    // Si no hay datos, devolver un valor predeterminado

  // Reducir los datos a una cadena de puntos que define la polilínea
  return amounts.value.reduce((acc, amount, i) => {
    const x = (300 / (total - 1)) * i; // Calcular la posición X proporcionalmente
    const y = amountToPixels(amount);  // Convertir el valor en una posición Y
    return `${acc} ${x},${y}`;         // Agregar el nuevo punto a la cadena
  }, `0,${amountToPixels(amounts.value.length ? amounts.value[0]:0)}`);
});

// Reactive refs para el puntero de la línea vertical
const showPointer = ref(false); // Controlar si la línea vertical se muestra
const pointer = ref(0);   // Posición X de la línea vertical

const emit = defineEmits(["select"]);

watch (pointer,(value)=> {
    const index = Math.ceil((value/(300 / amounts.value.length)));
    if (index < 0 || index > amounts.value.length);
    emit("select",amounts.value[index - 1])

    

});
//const emit = defineEmits(["select"])

// Función para manejar la interacción táctil y mover la línea vertical
const tap = ({target, touches}) => {
  showPointer.value = true;  // Mostrar la línea vertical
  const elementWidth = target.getBoundingClientRect().width; // Obtener el ancho del SVG
  const elementX = target.getBoundingClientRect().x;         // Obtener la posición X del SVG
  const touchX = touches[0].clientX;                         // Obtener la posición X del toque
  pointer.value = ((touchX - elementX) * 300) / elementWidth; // Calcular la posición X en el SVG
  

};

// Función para ocultar la línea vertical al terminar la interacción táctil
const untap = () => {
  showPointer.value = false; // Ocultar la línea vertical
};
</script>

<style scoped>
/* Contenedor principal del gráfico */
.chart-container {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
  padding: 1.5rem;
  background-color: #f9f9f9;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  text-align: center;
}

/* Estilo para el SVG */
.chart {
  width: 100%;
  height: auto;
}

/* Línea base */
.base-line {
  stroke: #c4c4c4;
  stroke-width: 3;
}

/* Línea de datos */
.data-line {
  fill: none;
  stroke: #0689b0;
  stroke-width: 2;
  stroke-linejoin: round;
  stroke-linecap: round;
}

/* Línea vertical */
.vertical-line {
  stroke: #04b500;
  stroke-width: 3;
  stroke-dasharray: 4 2; /* Línea punteada */
}

/* Estilo para el texto descriptivo */
.chart-caption {
  margin-top: 1.5rem;
  font-size: 1rem;
  color: #333;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}
</style>
