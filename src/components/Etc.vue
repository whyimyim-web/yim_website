<template>
  <section id="etc">
    <div class="container">
      <div class="collection-header">
        <h2 class="section-title libertine-title">ETC</h2>
        <span>Edition 02</span>
      </div>

      <swiper
        :modules="modules"
        :slides-per-view="3"
        :space-between="56"
        :breakpoints="breakpoints"
        navigation
        class="collection-grid"
      >
        <swiper-slide v-for="product in products" :key="product.id" class="object-card">
          <div class="object-image" :style="{ backgroundImage: getImagePath(product.image) }"></div>
          <div class="object-meta">
            <h3>{{ product.name }}</h3>
            <span v-if="product.size" class="size">{{ product.size }}</span>
          </div>
          <div class="price">{{ product.price }}</div>
          <a href="#" class="detail-link">View details →</a>
        </swiper-slide>
      </swiper>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'
import { Swiper, SwiperSlide } from 'swiper/vue'
import { Navigation } from 'swiper/modules'
import 'swiper/css'
import 'swiper/css/navigation'

const products = ref([])
const basePath = import.meta.env.BASE_URL

const modules = [Navigation]

const breakpoints = {
  320: {
    slidesPerView: 1,
    spaceBetween: 20,
    slidesPerGroup: 1,
  },
  900: {
    slidesPerView: 2,
    spaceBetween: 40,
    slidesPerGroup: 2,
  },
  1200: {
    slidesPerView: 3,
    spaceBetween: 56,
    slidesPerGroup: 3,
  },
}

const getImagePath = computed(() => {
  return (filename) => {
    return filename ? `url(${basePath}assets/images/${filename})` : 'none'
  }
})

onMounted(async () => {
  try {
    const res = await fetch(`${basePath}data/etc_products.json?v=${import.meta.env.VITE_BUILD_TIME}`)
    const data = await res.json()
    products.value = data.products
  } catch (error) {
    console.error('Failed to load etc products:', error)
  }
})
</script>

<style scoped>
.collection-grid {
  width: 100%;
}

.object-image {
  aspect-ratio: 1 / 1;
}

:deep(.swiper-button-next),
:deep(.swiper-button-prev) {
  color: white;
  width: 28px;
  height: 28px;
  top: 43%;
  transform: translateY(-50%);
}

:deep(.swiper-button-next:after),
:deep(.swiper-button-prev:after) {
  font-size: 14px;
}

:deep(.swiper-button-next:hover),
:deep(.swiper-button-prev:hover) {
  color: white;
}

.libertine-title {
  font-family: 'LinLibertine', serif;
}
</style>
