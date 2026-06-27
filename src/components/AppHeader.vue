<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const scrolled = ref(false)
const menuOpen = ref(false)

const navLinks = [
  { href: '#story',    label: '想い' },
  { href: '#gallery',  label: 'メニュー' },
  { href: '#pricing',  label: '料金' },
  { href: '#process',  label: '流れ' },
  { href: '#faq',      label: 'FAQ' },
  { href: '#contact',  label: 'お問い合わせ' },
]

function handleScroll() { scrolled.value = window.scrollY > 60 }
function toggleMenu() { menuOpen.value = !menuOpen.value }
function closeMenu() { menuOpen.value = false }

function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function smoothScroll(e, href) {
  e.preventDefault()
  closeMenu()
  document.querySelector(href)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}

onMounted(() => window.addEventListener('scroll', handleScroll, { passive: true }))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<template>
  <header class="header" :class="{ scrolled }">
    <div class="inner container">
      <a href="#" class="logo" @click.prevent="scrollToTop">
        <span class="june">JUNE</span>
        <span class="berry">Berry</span>
      </a>

      <nav class="nav" :class="{ open: menuOpen }" aria-label="メインナビゲーション">
        <ul>
          <li v-for="link in navLinks" :key="link.href">
            <a :href="link.href" @click="(e) => smoothScroll(e, link.href)">{{ link.label }}</a>
          </li>
        </ul>
      </nav>

      <button class="toggle" :aria-expanded="menuOpen.toString()" aria-label="メニューを開く" @click="toggleMenu">
        <span /><span /><span />
      </button>
    </div>

    <Transition name="overlay">
      <div v-if="menuOpen" class="overlay" @click="closeMenu" />
    </Transition>
  </header>
</template>

<style scoped>
.header {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 100;
  padding: 1.2rem 0;
  background: rgba(255, 248, 251, 0.95);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border-bottom: 1px solid rgba(191, 78, 120, 0.1);
  transition: box-shadow var(--transition), padding var(--transition);
}

.header.scrolled {
  box-shadow: 0 2px 20px rgba(191, 78, 120, 0.1);
  padding: 0.85rem 0;
}

.inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

/* Logo */
.logo { display: inline-flex; align-items: baseline; gap: 0.2em; }

.june {
  font-family: var(--font-serif);
  font-size: 1.35rem;
  font-weight: 600;
  letter-spacing: 0.12em;
  color: var(--gold);
}

.berry {
  font-family: var(--font-serif);
  font-style: italic;
  font-size: 1.3rem;
  font-weight: 300;
  color: var(--purple);
}

/* Nav */
.nav ul { display: flex; gap: 2.2rem; }

.nav a {
  font-size: 0.78rem;
  letter-spacing: 0.1em;
  color: rgba(60, 20, 40, 0.6);
  position: relative;
  padding-bottom: 3px;
  transition: color var(--transition);
}

.nav a::after {
  content: '';
  position: absolute;
  bottom: 0; left: 0;
  width: 0; height: 1px;
  background: var(--gold);
  transition: width var(--transition);
}

.nav a:hover { color: var(--gold); }
.nav a:hover::after { width: 100%; }

/* Toggle */
.toggle {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
  z-index: 101;
}

.toggle span {
  display: block;
  width: 22px; height: 1.5px;
  background: var(--gold);
  border-radius: 2px;
  transition: transform var(--transition), opacity var(--transition);
}

.toggle[aria-expanded="true"] span:nth-child(1) { transform: translateY(6.5px) rotate(45deg); }
.toggle[aria-expanded="true"] span:nth-child(2) { opacity: 0; }
.toggle[aria-expanded="true"] span:nth-child(3) { transform: translateY(-6.5px) rotate(-45deg); }

/* Overlay */
.overlay {
  position: fixed;
  inset: 0;
  background: rgba(60, 20, 40, 0.35);
  z-index: 89;
  backdrop-filter: blur(4px);
}

.overlay-enter-active, .overlay-leave-active { transition: opacity var(--transition); }
.overlay-enter-from, .overlay-leave-to { opacity: 0; }

/* Mobile */
@media (max-width: 768px) {
  .toggle { display: flex; }

  .nav {
    position: fixed;
    top: 0; right: -100%;
    width: min(320px, 80vw);
    height: 100svh;
    background: #fff8fb;
    padding: 6rem 2rem 2rem;
    transition: right var(--transition);
    z-index: 90;
    border-left: 1px solid rgba(191, 78, 120, 0.1);
  }

  .nav.open { right: 0; }

  .nav ul { flex-direction: column; gap: 0; }

  .nav a {
    display: block;
    padding: 1.1rem 0;
    font-size: 1rem;
    border-bottom: 1px solid rgba(191, 78, 120, 0.08);
    color: rgba(60, 20, 40, 0.65);
  }

  .nav a::after { display: none; }
}
</style>
