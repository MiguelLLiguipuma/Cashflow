<template>
  <div class="splashscreen">
    <img 
      src="@/assets/cashflow-icon.svg"
      alt="Logo"
      class="logo">

    <h1 class="title"><span>Cash</span>Flow</h1>
  </div>
</template>

<style scoped>
.splashscreen {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
  background-color: #fff;
}

.logo {
  width: 150px;
  height: 150px;
  animation: fadeIn 2s ease-out, scaleUp 2s ease-out;
}

.title {
  color: var(--brand-blue);
  margin-top: 20px;
  opacity: 0;
  transform: translateY(20px);
  animation: fadeInTitle 2s ease-out 0.5s forwards, slideUp 2s ease-out 0.5s forwards;
}

.title span {
  color: var(--brand-green);
}

/* Animaciones */
@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes fadeInTitle {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes slideUp {
  0% {
    transform: translateY(20px);
  }
  100% {
    transform: translateY(0);
  }
}

@keyframes scaleUp {
  0% {
    transform: scale(0.8);
  }
  100% {
    transform: scale(1);
  }
}
</style>
