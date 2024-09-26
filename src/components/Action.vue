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
          <form @submit.prevent="submit">
            <div class="field">
              <label for="title">Título</label>
              <input type="text" id="title" v-model="title" class="input-field" required>
            </div>
            <div class="field">
              <label for="amount">Monto</label>
              <input type="number" id="amount" v-model="amount" class="input-field" required>
            </div>
            <div class="field">
              <label for="description">Descripción</label>
              <textarea rows="4" id="description" v-model="description" class="input-field"></textarea>
            </div>
            <div class="field radio-group">
              <label class="radio-label">
                <input type="radio" v-model="movementType" value="Ingreso" />
                <span>Ingreso</span>
              </label>
              <label class="radio-label">
                <input type="radio" v-model="movementType" value="Gasto" />
                <span>Gasto</span>
              </label>
            </div>
            <div class="action">
              <button class="submit-btn">Agregar movimiento</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const showModal = ref(false);
const title = ref("");
const amount = ref(0);
const description = ref("");
const movementType = ref("Ingreso");
const errors = ref({}); // Para almacenar errores de validación


const emit = defineEmits(["create"]);

const closeModal = () => {
  showModal.value = false;
  resetForm();
};

const resetForm = () => {
  title.value = "";
  description.value = "";
  amount.value = 0;
  movementType.value = "Ingreso";
  errors.value = {}; // Limpia los errores
};


const submit = () => {
  errors.value = {}; // Resetea los errores

  // Validación
  if (!title.value.trim()) {
    errors.value.title = "El título es requerido.";
  }
  if (!amount.value) {
    errors.value.amount = "El monto es requerido.";
  }

  // Si hay errores, no se envía el formulario
  if (Object.keys(errors.value).length) return;

  emit("create", {
    title: title.value,
    description: description.value,
    amount: movementType.value === "Ingreso" ? amount.value : -amount.value,
    time: new Date().getTime(),
    id: new Date(),
  });
  
  closeModal(); // Cierra el modal si no hay errores
};
</script>

<style scoped>
/* Botón principal */
.primary-btn {
  color: white;
  background-color: var(--brand-blue);
  padding: 12px 24px;
  border: none;
  border-radius: 8px;
  font-size: 1.1rem;
  cursor: pointer;
  font-weight: 600;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s ease, transform 0.2s ease, box-shadow 0.2s ease;
}

.primary-btn:hover {
  background-color: #004080;
  transform: translateY(-3px);
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.2);
}

/* Overlay del modal */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6);
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
  border-radius: 12px;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15);
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
  border-bottom: 2px solid #004080;
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
  align-items: stretch; /* Cambiado a stretch para que los campos ocupen el ancho total */
  justify-content: center;
}

.field {
  margin-bottom: 16px; /* Espaciado entre campos */
}

.input-field {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  transition: border-color 0.3s ease;
}

.input-field:focus {
  border-color: var(--brand-blue);
  outline: none; /* Evita el contorno por defecto del navegador */
}

/* Estilos de los botones */
.submit-btn {
  color: white;
  background-color: var(--brand-blue);
  border: none;
  border-radius: 5px;
  padding: 10px 20px;
  font-size: 1.1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.submit-btn:hover {
  background-color: #004080;
 

  
}
</style>



