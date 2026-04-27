<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container-fluid">
      <NuxtLink class="navbar-brand" to="/">KinoTower</NuxtLink>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse justify-content-end" id="navbarNav">
        <div class="navbar-nav">
          <template v-if="isLoggedIn">
            <NuxtLink class="nav-link" to="/profile">{{ userName }}</NuxtLink>
            <a class="nav-link" href="#" @click.prevent="logout">Exit</a>
          </template>
          <template v-else>
            <NuxtLink class="nav-link" to="/SignUp">Sign Up</NuxtLink>
            <NuxtLink class="nav-link" to="/SignIn">Sign In</NuxtLink>
          </template>
        </div>
      </div>
    </div>
  </nav>

  <div class="container mt-4">
    <slot />
  </div>

  <footer class="footer mt-auto py-3 bg-light">
    <div class="container text-center">
      <p class="mb-0">&copy; 2025 KinoTower. All rights reserved.</p>
    </div>
  </footer>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

const isLoggedIn = ref(false)
const userName = ref('User')

function logout() {
  isLoggedIn.value = false
}
</script>

<style>

</style>