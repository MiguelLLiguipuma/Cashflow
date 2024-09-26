<template>
  <header class="header">
    <div class="header-container" @click="reload">
      <img src="@/assets/cashflow-icon.svg" alt="CashFlow Logo" class="logo" />
      <h1><span>Cash</span>Flow</h1>
    </div>
  </header>
</template>

<script>
export default {
  methods: {
    reload() {
      location.reload();
    }
  },
};
</script>

<style scoped>
.header {
  display: flex;
  justify-content: center; /* Center the header content */
  align-items: center;
  padding: 1rem 2rem;
  background-color: #f8f9fa; /* Keep the light background color */
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1); /* Slightly larger shadow for depth */
  width: 100%;
  position: sticky; /* Make the header stick to the top */
  top: 0;
  z-index: 10; /* Ensure it's above other content */
}

.header-container {
  display: flex;
  align-items: center;
  cursor: pointer;
  transition: transform 0.3s ease; /* Add smooth transition */
}

.header-container:hover {
  transform: scale(1.05); /* Slight scale on hover */
}

.logo {
  width: 50px; /* Slightly larger logo */
  height: 50px;
  margin-right: 1rem;
  transition: transform 0.3s ease, filter 0.3s ease; /* Smooth hover effect */
}

.logo:hover {
  transform: scale(1.15); /* Increase scale on hover */
  filter: brightness(1.2); /* Brighten the logo */
}

h1 {
  font-size: 1.8rem; /* Slightly larger font size */
  color: var(--brand-blue, #0689b0);
  margin: 0;
  font-family: 'Roboto', sans-serif; /* Clean and modern font */
  letter-spacing: 1px; /* Improve readability */
  transition: color 0.3s ease; /* Smooth color transition */
}

h1 span {
  color: var(--brand-green, #04b500);
  font-weight: bold;
}

h1:hover {
  color: #036a90; /* Change title color on hover */
}
</style>
