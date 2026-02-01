<template>
  <section id="atelier">
    <div class="container atelier-grid">
      <div>
        <h2 class="section-title">Atelier</h2>
        <p>
          Yi'm의 작업은 느린 리듬 속에서 이루어집니다. 하나의 오브제가 완성되기까지
          수십 번의 수정과 판단이 반복됩니다.
        </p>
      </div>
      <div class="atelier-gallery">
        <div v-for="(image, index) in atelier.images" :key="index" class="atelier-img" :style="{ backgroundImage: `url(${basePath}assets/images/${image})` }"></div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const basePath = import.meta.env.BASE_URL
const atelier = ref({
  images: []
})

onMounted(async () => {
  try {
    const basePath = import.meta.env.BASE_URL
    const res = await fetch(`${basePath}data/site-data.json`)
    const data = await res.json()
    atelier.value = data.atelier
  } catch (error) {
    console.error('Failed to load atelier data:', error)
  }
})
</script>
