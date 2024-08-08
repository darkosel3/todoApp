<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <header>
    <div class="header-div">
      <nav>
        <RouterLink to="/">Home</RouterLink>
      </nav>
      <h1 class="title">Do It Today!</h1>
    </div>
  </header>
  <div class="container">
    <RouterView />
  </div>
</template>

<style scoped>
a[href^="/"] {
  text-decoration: none;
  color: white;
}
</style>
