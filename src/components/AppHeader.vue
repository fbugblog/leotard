<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const scrolled = ref(false)
const menuOpen = ref(false)

const navLinks = [
  { href: '#concept', label: 'コンセプト' },
  { href: '#products', label: 'コレクション' },
  { href: '#features', label: '特徴' },
  { href: '#contact', label: 'お問い合わせ' },
]

function handleScroll() {
  scrolled.value = window.scrollY > 50
}

function toggleMenu() {
  menuOpen.value = !menuOpen.value
}

function closeMenu() {
  menuOpen.value = false
}

function smoothScroll(e, href) {
  e.preventDefault()
  closeMenu()
  const el = document.querySelector(href)
  el?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}

onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<template>
  <header class="site-header" :class="{ scrolled }">
    <div class="header-inner container">
      <a href="#" class="logo" @click.prevent="window.scrollTo({ top: 0, behavior: 'smooth' })">
        <span class="logo-june">June</span>
        <span class="logo-berry">BERRY</span>
      </a>

      <nav class="nav" :class="{ 'nav--open': menuOpen }" aria-label="メインナビゲーション">
        <ul>
          <li v-for="link in navLinks" :key="link.href">
            <a :href="link.href" @click="(e) => smoothScroll(e, link.href)">
              {{ link.label }}
            </a>
          </li>
        </ul>
      </nav>

      <button
        class="nav-toggle"
        :aria-expanded="menuOpen.toString()"
        aria-label="メニューを開く"
        @click="toggleMenu"
      >
        <span></span>
        <span></span>
        <span></span>
      </button>
    </div>

    <!-- Mobile overlay -->
    <Transition name="overlay">
      <div v-if="menuOpen" class="nav-overlay" @click="closeMenu" />
    </Transition>
  </header>
</template>

<style scoped>
.site-header {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 100;
  padding: 1.2rem 0;
  transition: background var(--transition), box-shadow var(--transition), padding var(--transition);
}

.site-header.scrolled {
  background: rgba(253, 248, 245, 0.95);
  backdrop-filter: blur(12px);
  box-shadow: var(--shadow-sm);
  padding: 0.7rem 0;
}

.header-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.logo {
  display: inline-flex;
  align-items: baseline;
  gap: 0.2em;
  z-index: 101;
  position: relative;
}

.logo-june {
  font-family: var(--font-serif);
  font-style: italic;
  font-size: 1.5rem;
  font-weight: 300;
  color: var(--berry);
}

.logo-berry {
  font-family: var(--font-serif);
  font-size: 1.3rem;
  font-weight: 600;
  letter-spacing: 0.12em;
  color: var(--berry-light);
}

.nav ul {
  display: flex;
  gap: 2.5rem;
}

.nav a {
  font-size: 0.85rem;
  letter-spacing: 0.08em;
  color: var(--text);
  position: relative;
  padding-bottom: 3px;
  transition: color var(--transition);
}

.nav a::after {
  content: '';
  position: absolute;
  bottom: 0; left: 0;
  width: 0; height: 1px;
  background: var(--berry);
  transition: width var(--transition);
}
.nav a:hover { color: var(--berry); }
.nav a:hover::after { width: 100%; }

.nav-toggle {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
  z-index: 101;
  position: relative;
}

.nav-toggle span {
  display: block;
  width: 24px; height: 2px;
  background: var(--berry);
  border-radius: 2px;
  transition: transform var(--transition), opacity var(--transition);
}

.nav-toggle[aria-expanded="true"] span:nth-child(1) { transform: translateY(7px) rotate(45deg); }
.nav-toggle[aria-expanded="true"] span:nth-child(2) { opacity: 0; transform: scaleX(0); }
.nav-toggle[aria-expanded="true"] span:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }

.nav-overlay {
  position: fixed;
  inset: 0;
  background: rgba(44, 26, 36, 0.4);
  z-index: 89;
}

.overlay-enter-active, .overlay-leave-active { transition: opacity var(--transition); }
.overlay-enter-from, .overlay-leave-to { opacity: 0; }

@media (max-width: 768px) {
  .nav-toggle { display: flex; }

  .nav {
    position: fixed;
    top: 0; right: -100%;
    width: min(320px, 80vw);
    height: 100svh;
    background: var(--white);
    box-shadow: -4px 0 32px rgba(0, 0, 0, 0.1);
    padding: 6rem 2rem 2rem;
    transition: right var(--transition);
    z-index: 90;
  }

  .nav--open { right: 0; }

  .nav ul {
    flex-direction: column;
    gap: 0;
  }

  .nav a {
    display: block;
    padding: 1rem 0;
    font-size: 1.1rem;
    border-bottom: 1px solid var(--berry-pale);
  }

  .nav a::after { display: none; }
}
</style>
