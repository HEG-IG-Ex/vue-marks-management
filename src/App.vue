<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header class="item-a">
    <img alt="Heg logo" class="logo" src="@/assets/heg-ge_01.webp" />
    <div class="nav-wrapper">
      <nav>
        <RouterLink to="/" class="nav-link">View</RouterLink>
        <RouterLink to="/capture" class="nav-link">Capture</RouterLink>
        <RouterLink to="/about" class="nav-link">About</RouterLink>
      </nav>
    </div>
  </header>
  <main class="item-b">
    <RouterView />
  </main>
</template>

<style scoped>
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 20px;
}

.logo {
  grid-area: header;
  width: 200px; /* adjust as needed */
  height: auto;
}

.nav-wrapper {
  grid-area: header;
}
.nav-link {
  margin-right: 20px; /* Adjust the spacing as needed */
}
</style>
