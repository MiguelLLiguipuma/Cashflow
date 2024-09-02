<template>
    <main>

        <p>{{ labelVisual }}</p>
        <h1>{{ amountCurrency }}</h1>
        <div class="graphic">
            <slot name="graphic"></slot> 
        </div>
        <div>
            <slot name="action"></slot>
        </div>


    </main>

</template>
<script>

const currencyFormatter = new Intl.NumberFormat("es-EC", {
  style: "currency",
  currency: "USD",
});

export default{
    props: {
        totalLabel:{
            type: String,

        },
        label:{
            type: String
        },
        totalAmount:{
            type: Number

        },
        amount: {
            type: Number,
            default: null,
        },
        
    },
    computed:{
            labelVisual(){
                return this.label !== null ? this.label : this.totalLabel;

            },
            amountVisual(){
                return this.amount !== null ? this.amount : this.totalAmount;
            },
            amountCurrency(){
                return currencyFormatter.format(this.amountVisual)
            }

        },
};

</script>

<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
  min-height: 100vh; /* Asegura que el contenido ocupe toda la altura de la pantalla */
  padding: 20px; /* Añade un poco de espacio alrededor */
  background-color: #f8f9fa; /* Color de fondo ligero para un look más profesional */
  box-sizing: border-box; /* Asegura que el padding se incluya en el ancho/alto */
}

h1,
p {
  margin: 0;
  text-align: center;
  color: #333; /* Color de texto más neutro y profesional */
}

h1 {
  margin-top: 20px; /* Espacio mayor para una separación más visual */
  font-size: 2rem; /* Aumenta el tamaño de la fuente para mayor impacto */
  font-weight: bold; /* Hace el título más prominente */
  color: var(--brand-green, #28a745); /* Usa una variable de color con un valor de respaldo */
}

p {
  margin-top: 10px; /* Añade un pequeño espacio superior para separación */
  font-size: 1.2rem; /* Tamaño de fuente mayor para mejor legibilidad */
  color: #555; /* Color de texto para diferenciar del título */
}

.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  max-width: 1200px; /* Limita el ancho máximo para mejor legibilidad en pantallas grandes */
  padding: 48px 24px;
  margin-top: 20px; /* Añade espacio entre el contenido y el gráfico */
  box-sizing: border-box;
  background-color: #ffffff; /* Fondo blanco para destacar el gráfico */
  border-radius: 8px; /* Bordes redondeados para un aspecto más moderno */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Sombra sutil para dar profundidad */
}
</style>
