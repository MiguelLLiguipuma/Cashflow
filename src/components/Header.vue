<template>
  <header class="header">
    <div class="header-container" @click="reload">
      <img src="@/assets/cashflow-icon.svg" alt="CashFlow Logo" class="logo" />
      <h1><span>Cash</span>Flow</h1>
    </div>
    <nav>
      <!-- Add any additional nav elements or buttons here -->
    </nav>
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
  justify-content: space-between; /* Adjusted for better layout */
  align-items: center;
  padding: 1rem 2rem; /* Added padding */
  background-color: #f8f9fa; /* Light background color */
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); /* Subtle shadow for depth */
  width: 100%;
}

.header-container {
  display: flex;
  align-items: center;
  cursor: pointer;
}

.logo {
  width: 48px;
  height: 48px;
  margin-right: 1rem; /* Spacing between logo and title */
  transition: transform 0.3s ease; /* Smooth hover effect */
}

.logo:hover {
  transform: scale(1.1); /* Slight scale-up on hover */
}

h1 {
  font-size: 1.6rem;
  color: var(--brand-blue, #0689b0);
  margin: 0;
  transition: color 0.3s ease; /* Smooth color transition on hover */
}

h1 span {
  color: var(--brand-green, #04b500);
  font-weight: bold; /* Emphasize the "Cash" part */
}

h1:hover {
  color: #036a90; /* Change title color on hover */
}


</style>
