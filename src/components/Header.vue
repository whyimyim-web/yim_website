<template>
  <header>
    <div class="container header-inner">
      <img class="logo" :src="`${basePath}assets/logo/logo.png`" alt="Yi'm logo">
      <nav>
        <a href="#collection">Collection</a>
        <a href="#concept">Concept</a>
        <a href="#atelier">Atelier</a>
        <a href="#contact">Contact</a>
      </nav>
    </div>
  </header>
</template>

<script setup>
const basePath = import.meta.env.BASE_URL
</script>
