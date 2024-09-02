<template>
  <teleport to="body">
    <div class="modal-overlay" @click="closeModal">
      <div class="modal" @click.stop>
        <div class="head">
          <p class="title">Nuevo Movimiento</p>
          <div class="actions">
            <img @click="close" src="@/assets/trash-icon.svg" alt="cerrar" class="icon-btn" />
            <button class="close-btn" @click="closeModal">✖</button>
          </div>
        </div>
        <div class="content">
          <!-- Contenido del modal -->
          <slot></slot>
        </div>
      </div>
    </div>
  </teleport>
</template>

<script setup>
import { defineEmits } from "vue";

const emit = defineEmits(["close"]);
const close = () => emit("close");
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal {
  background-color: #fff;
  width: 90%;
  max-width: 500px;
  border-radius: 8px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  animation: slideIn 0.3s ease-out;
  z-index: 1001;
}

.head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 24px;
  background-color: var(--brand-blue);
  color: #fff;
}

.title {
  margin: 0;
  font-size: 1.5rem;
  font-weight: 600;
}
.actions {
  display: flex;
  align-items: center;
}

.icon-btn {
  margin-right: 12px;
  width: 24px;
  height: 24px;
  cursor: pointer;
}

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

.content {
  padding: 24px;
  font-size: 1rem;
  color: #333;
  line-height: 1.5;
}

@keyframes slideIn {
  from {
    transform: translateY(-20px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}
</style>
