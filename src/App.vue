<template>
  <!-- Header -->
  <header>
    <div class="container header-inner">
      <div class="logo">Yi'm</div>
      <nav>
        <a href="#collection">Collection</a>
        <a href="#concept">Concept</a>
        <a href="#atelier">Atelier</a>
        <a href="#contact">Contact</a>
      </nav>
    </div>
  </header>

  <!-- Hero -->
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
      <div class="hero-visual">Signature Object</div>
    </div>
  </section>

  <!-- Collection -->
  <section id="collection">
    <div class="container">
      <div class="collection-header">
        <h2 class="section-title">Collection</h2>
        <span>Edition 01</span>
      </div>
      <div class="collection-grid">
        <div v-for="product in products" :key="product.id" class="object-card">
          <div class="object-image"></div>
          <div class="object-meta">
            <h3>{{ product.name }}</h3>
            <span v-if="product.badge" class="badge">{{ product.badge }}</span>
          </div>
          <div class="price">{{ product.price }}</div>
          <a href="#" class="detail-link">View details →</a>
        </div>
      </div>
    </div>
  </section>

  <!-- Concept -->
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
      <div class="concept-visual"></div>
    </div>
  </section>

  <!-- Atelier -->
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
        <div class="atelier-img"></div>
        <div class="atelier-img"></div>
        <div class="atelier-img"></div>
        <div class="atelier-img"></div>
      </div>
    </div>
  </section>

  <!-- Contact -->
  <section id="contact" class="contact">
    <div class="container">
      <h2 class="section-title">Contact</h2>
      <p>Collaboration, commissions, and partnerships</p>
      <div class="contact-buttons">
        <a href="mailto:contact@yim.com" class="btn btn-primary">Send Email</a>
        <a href="#" class="btn btn-outline">Instagram</a>
      </div>
    </div>
  </section>

  <!-- Footer -->
  <footer>
    <div class="container footer-grid">
      <div>
        <div class="logo">Yi'm</div>
        <p>Ceramic Objects & Contemporary Forms</p>
      </div>
      <div class="footer-links">
        <a href="#">Instagram</a>
        <a href="#">Policy</a>
        <a href="#">Terms</a>
      </div>
    </div>
    <div class="container copyright">© 2026 Yi'm. All rights reserved.</div>
  </footer>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const products = ref([])

onMounted(async () => {
  try {
    const res = await fetch('/data/products.json')
    const data = await res.json()
    products.value = data.products
  } catch (error) {
    console.error('Failed to load products:', error)
    // Fallback to default products
    products.value = [
      {
        id: 1,
        name: 'Object 01',
        badge: 'Limited',
        price: '₩120,000',
      },
      {
        id: 2,
        name: 'Object 02',
        badge: 'Limited',
        price: '₩120,000',
      },
      {
        id: 3,
        name: 'Object 03',
        badge: 'Limited',
        price: '₩120,000',
      },
    ]
  }
})
</script>
