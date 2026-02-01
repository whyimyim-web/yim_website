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
      <swiper
        :modules="modules"
        :slides-per-view="2"
        :space-between="40"
        :breakpoints="breakpoints"
        navigation
        class="atelier-gallery"
      >
        <swiper-slide v-for="(image, index) in atelier.images" :key="index" class="atelier-img" :style="{ backgroundImage: `url(${basePath}assets/images/${image})` }"></swiper-slide>
      </swiper>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Swiper, SwiperSlide } from 'swiper/vue'
import { Navigation } from 'swiper/modules'
import 'swiper/css'
import 'swiper/css/navigation'

const basePath = import.meta.env.BASE_URL
const atelier = ref({
  images: []
})

const modules = [Navigation]

const breakpoints = {
  320: {
    slidesPerView: 1,
    spaceBetween: 20,
  },
  900: {
    slidesPerView: 2,
    spaceBetween: 40,
  },
}

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

<style scoped>
.atelier-gallery {
  width: 100%;
}

:deep(.swiper-button-next),
:deep(.swiper-button-prev) {
  color: var(--text);
  width: 40px;
  height: 40px;
}

:deep(.swiper-button-next:after),
:deep(.swiper-button-prev:after) {
  font-size: 18px;
}

:deep(.swiper-button-next:hover),
:deep(.swiper-button-prev:hover) {
  color: var(--point);
}
</style>
