<template>
  <section class="hero">
    <div class="container hero-grid">
      <div>
        <small>Ceramic Objects</small>
        <h1>Silence in form.</h1>
        <p>
          Yi'm은 기능을 넘어선 형태의 의미를 탐구합니다.
          절제된 조형과 물성의 균형 속에서 오브제는 하나의 태도가 됩니다.
        </p>
        <div class="hero-buttons">
          <a href="#collection" class="btn btn-primary">View Objects</a>
          <a href="#concept" class="btn btn-outline">Philosophy</a>
        </div>
      </div>
      <div class="hero-visual" :style="{ backgroundImage: hero.images?.[0] ? `url(${basePath}assets/images/${hero.images[0]})` : 'none' }"></div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const basePath = import.meta.env.BASE_URL
const hero = ref({
  images: []
})

onMounted(async () => {
  try {
    const basePath = import.meta.env.BASE_URL
    const res = await fetch(`${basePath}data/site-data.json`)
    const data = await res.json()
    hero.value = data.hero
  } catch (error) {
    console.error('Failed to load hero data:', error)
  }
})
</script>
