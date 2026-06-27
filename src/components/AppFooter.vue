<script setup>
const navLinks = [
  { href: '#concept', label: 'コンセプト' },
  { href: '#products', label: 'コレクション' },
  { href: '#features', label: '特徴' },
  { href: '#contact', label: 'お問い合わせ' },
]

const legalLinks = [
  { href: '#', label: '特定商取引法に基づく表記' },
  { href: '#', label: 'プライバシーポリシー' },
  { href: '#', label: '返品・交換について' },
  { href: '#', label: 'サイズガイド' },
]

function smoothScroll(e, href) {
  e.preventDefault()
  const el = document.querySelector(href)
  el?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}
</script>

<template>
  <footer class="site-footer">
    <div class="container">
      <div class="top">
        <div class="brand">
          <p class="logo">
            <span class="logo-june">June</span>
            <span class="logo-berry">BERRY</span>
          </p>
          <p class="tagline">纏うほどに、輝きが増す。</p>
        </div>

        <nav class="nav" aria-label="フッターナビゲーション">
          <ul>
            <li v-for="link in navLinks" :key="link.label">
              <a :href="link.href" @click="(e) => smoothScroll(e, link.href)">{{ link.label }}</a>
            </li>
          </ul>
          <ul>
            <li v-for="link in legalLinks" :key="link.label">
              <a :href="link.href">{{ link.label }}</a>
            </li>
          </ul>
        </nav>
      </div>

      <div class="bottom">
        <p>&copy; 2024 June BERRY. All rights reserved.</p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.site-footer {
  background: var(--text);
  color: rgba(255, 255, 255, 0.7);
  padding-block: 3rem 1.5rem;
}

.top {
  display: flex;
  justify-content: space-between;
  gap: 3rem;
  margin-bottom: 2.5rem;
  flex-wrap: wrap;
}

.logo {
  display: flex;
  align-items: baseline;
  gap: 0.2em;
  margin-bottom: 0.5rem;
}

.logo-june {
  font-family: var(--font-serif);
  font-style: italic;
  font-size: 1.8rem;
  font-weight: 300;
  color: var(--pink);
}

.logo-berry {
  font-family: var(--font-serif);
  font-size: 1.5rem;
  font-weight: 600;
  letter-spacing: 0.15em;
  color: var(--berry-pale);
}

.tagline {
  font-family: var(--font-serif);
  font-style: italic;
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.4);
}

.nav {
  display: flex;
  gap: 4rem;
}

.nav ul {
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}

.nav a {
  font-size: 0.82rem;
  color: rgba(255, 255, 255, 0.6);
  letter-spacing: 0.04em;
  transition: color var(--transition);
}

.nav a:hover { color: var(--pink); }

.bottom {
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding-top: 1.5rem;
  text-align: center;
  font-size: 0.75rem;
  color: rgba(255, 255, 255, 0.35);
}

@media (max-width: 768px) {
  .top { flex-direction: column; gap: 2rem; }
  .nav { gap: 2rem; }
}
</style>
