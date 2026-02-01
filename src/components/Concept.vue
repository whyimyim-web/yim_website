<template>
  <section id="concept" class="concept">
    <div class="container concept-grid">
      <div>
        <h2 class="section-title">Concept</h2>
        <p>
          Yi'm은 완성보다 과정, 결과보다 선택을 중요하게 생각합니다.
          모든 형태는 기능에서 출발하지만, 그 끝은 감각과 태도에 닿습니다.
        </p>
        <p>
          흙, 유약, 시간은 Yi'm의 언어입니다. 우리는 불필요한 장식을 제거하고,
          오직 형태와 비례만으로 오브제를 정의합니다.
        </p>
      </div>
      <div class="concept-visual" :style="{ backgroundImage: concept.images?.[0] ? `url(${basePath}assets/images/${concept.images[0]})` : 'none' }"></div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const basePath = import.meta.env.BASE_URL
const concept = ref({
  images: []
})

onMounted(async () => {
  try {
    const basePath = import.meta.env.BASE_URL
    const res = await fetch(`${basePath}data/site-data.json`)
    const data = await res.json()
    concept.value = data.concept
  } catch (error) {
    console.error('Failed to load concept data:', error)
  }
})
</script>
