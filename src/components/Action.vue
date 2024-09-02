<template>
  <button @click="showModal = true" class="primary-btn">Agregar movimiento</button>
  <Teleport to="body">
    <div v-if="showModal" class="modal-overlay" @click="closeModal">
      <div class="modal" @click.stop>
        <div class="head">
          <p class="title">Nuevo Movimiento</p>
          <button class="close-btn" @click="closeModal">✖</button>
        </div>
        <div class="modal-content">
          <!-- Contenido del formulario dentro del modal -->
          <form @submit.prevent="submit">
            <div class="field">
              <label for="title">Titulo</label>
              <input type="text" id="title" v-model="title">
            </div>
            <div class="field">
              <label for="amount">Monto</label>
              <input type="number" id="amount" v-model="amount">
            </div>
            <div class="field">
              <label for="description">Descripción</label>
              <textarea rows="4" id="description" v-model="description"></textarea>
            </div>
            <div class="field radio-group">
              <label class="radio-label">
                <input type="radio" v-model="movementType" value="Ingreso" />
                <span>Ingreso</span>
              </label>
              <label class="radio-label">
                <input type="radio" v-model="movementType" value="Gasto" />
                <span>Gastos</span>
              </label>
            </div>
            <div class="action">
              <button >Agregar movimiento</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<script setup >
import { ref,defineEmits } from "vue";
//import Modal from "./Modal.vue"

const showModal = ref(false);
const title = ref("");
const amount = ref(0);
const description = ref("");
const movementType = ref("Ingreso");

const emit = defineEmits(["create"]);

const closeModal = () => {
  showModal.value = false;
};


const submit = () => {
  // Lógica para procesar el formulario
  showModal.value = !showModal.value;
  emit("create",{
    title:title.value,
    description:description.value,
    amount:movementType.value === "Ingreso" ? amount.value : -amount.value,
    time: new Date().getTime(),
    id: new Date(),
  }); // Cierra el modal al enviar
  title.value = "";
  description.value ="";
  amount.value = 0;
  movementType.value = "Ingreso"
};
</script>

<style scoped>
/* Botón principal */
.primary-btn {
  color: white;
  background-color: var(--brand-blue);
  padding: 10px 20px;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

.primary-btn:hover {
  background-color: #004080;
  transform: translateY(-2px);
}

/* Overlay del modal */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6); /* Más opacidad para un enfoque más claro en el modal */
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

/* Contenedor del modal */
.modal {
  background-color: #fff;
  width: 90%;
  max-width: 500px;
  border-radius: 12px; /* Bordes más suaves para un diseño moderno */
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15); /* Sombras más profundas */
  overflow: hidden;
  z-index: 1001;
  animation: fadeIn 0.3s ease-out;
}

/* Encabezado del modal */
.head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 24px;
  background-color: var(--brand-blue);
  color: #fff;
  border-bottom: 2px solid #004080; /* Línea inferior para resaltar el encabezado */
}

.title {
  margin: 0;
  font-size: 1.5rem;
  font-weight: 600;
}

/* Botón de cerrar */
.close-btn {
  background: none;
  border: none;
  color: #fff;
  font-size: 1.5rem;
  cursor: pointer;
  transition: color 0.3s ease;
}

.close-btn:hover {
  color: #ff4d4f;
}

/* Contenido del modal */
.modal-content {
  padding: 24px;
  font-size: 1rem;
  color: #333;
  line-height: 1.5;
}

/* Estilos del formulario */
form {
  display: flex;
  flex-direction: column;
  align-items: center; /* Centra horizontalmente los elementos del formulario */
  justify-content: center;
  font-size: 1.2rem;
  width: 100%;
}

.field {
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;
  width: 100%;
}

label {
  margin-bottom: 8px;
  font-weight: 500;
  color: #004080; /* Color de etiqueta más claro para mejor contraste */
}

/* Ajustes generales para los campos de formulario */
.field input,
.field textarea {
  width: 100%;
  padding: 10px; /* Aumenta el padding para mayor comodidad */
  font-size: 1rem;
  border: 1px solid #ccc; /* Borde más delgado y ligero */
  border-radius: 8px;
  box-sizing: border-box;
  line-height: 1.5;
  transition: border-color 0.3s ease;
}

/* Ajuste específico para textarea */
.field textarea {
  min-height: 120px; /* Ajusta la altura mínima para que coincida mejor con el diseño */
  resize: vertical; /* Permite cambiar el tamaño verticalmente si es necesario */
}

/* Asegura que las etiquetas y los campos estén alineados correctamente */
.field {
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;
  align-items: flex-start; /* Alinea las etiquetas al principio de los campos */
}

/* Ajuste de los radio buttons */
.radio-group {
  display: flex;
  justify-content: space-around;
  width: 100%;
  margin-top: 16px;
  align-items: center;
}

.radio-label {
  display: flex;
  align-items: left;
  font-weight: 300;
}

.radio-label input {
  margin-right: 8px;
}


/* Estilo del botón de acción */
.action {
  display: flex;
  justify-content: center;
  width: 100%;
  margin-top: 24px;
}

/* Animaciones */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: scale(0.95);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}
</style>
