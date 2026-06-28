<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const scrolled = ref(false)
const menuOpen = ref(false)

const navLinks = [
  { href: '#concept',  label: 'コンセプト' },
  { href: '#programs', label: 'クラス' },
  { href: '#features', label: '特徴' },
  { href: '#contact',  label: 'お問い合わせ' },
]

function handleScroll() { scrolled.value = window.scrollY > 60 }
function toggleMenu() { menuOpen.value = !menuOpen.value }
function closeMenu() { menuOpen.value = false }
function scrollToTop() { window.scrollTo({ top: 0, behavior: 'smooth' }) }
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
      <a href="#" class="logo" @click.prevent="scrollToTop" aria-label="GRACE STUDIOトップへ">
        <span class="logo-mark" aria-hidden="true">G</span>
        <div class="logo-text">
          <span class="logo-name">GRACE</span>
          <span class="logo-sub">STUDIO</span>
        </div>
      </a>

      <nav class="nav" :class="{ open: menuOpen }" aria-label="メインナビゲーション">
        <ul>
          <li v-for="link in navLinks" :key="link.href">
            <a :href="link.href" @click="(e) => smoothScroll(e, link.href)">{{ link.label }}</a>
          </li>
        </ul>
        <button class="nav-cta btn btn-primary" @click="(e) => smoothScroll(e, '#contact')">
          体験予約
        </button>
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
  background: rgba(250, 250, 250, 0.9);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid transparent;
  transition: box-shadow var(--transition), padding var(--transition), border-color var(--transition);
}

.header.scrolled {
  box-shadow: var(--shadow-sm);
  padding: 0.8rem 0;
  border-bottom-color: var(--border);
}

.inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 2rem;
}

/* Logo */
.logo {
  display: inline-flex;
  align-items: center;
  gap: 0.7rem;
  flex-shrink: 0;
}

.logo-mark {
  width: 36px; height: 36px;
  border-radius: 10px;
  background: var(--pink);
  color: var(--surface);
  font-family: var(--font-display);
  font-size: 1.05rem;
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background var(--transition), transform var(--transition);
}

.logo:hover .logo-mark {
  background: var(--pink-700);
  transform: rotate(-5deg);
}

.logo-text {
  display: flex;
  flex-direction: column;
  line-height: 1;
  gap: 0.12em;
}

.logo-name {
  font-family: var(--font-display);
  font-size: 0.9rem;
  font-weight: 700;
  letter-spacing: 0.18em;
  color: var(--text);
}

.logo-sub {
  font-family: var(--font-display);
  font-size: 0.58rem;
  font-weight: 400;
  letter-spacing: 0.22em;
  color: var(--text-muted);
}

/* Nav */
.nav {
  display: flex;
  align-items: center;
  gap: 2.5rem;
}

.nav ul { display: flex; gap: 2rem; }

.nav a {
  font-family: var(--font-display);
  font-size: 0.76rem;
  font-weight: 400;
  letter-spacing: 0.04em;
  color: var(--text-mid);
  position: relative;
  padding-bottom: 2px;
  transition: color var(--transition);
}

.nav a::after {
  content: '';
  position: absolute;
  bottom: 0; left: 0;
  width: 0; height: 1.5px;
  background: var(--pink);
  transition: width var(--transition);
  border-radius: 2px;
}

.nav a:hover { color: var(--pink); }
.nav a:hover::after { width: 100%; }

.nav-cta { padding: 0.6em 1.4em; font-size: 0.76rem; }

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
  background: var(--text);
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
  background: rgba(26, 14, 22, 0.4);
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
    background: var(--surface);
    padding: 6rem 2rem 2rem;
    flex-direction: column;
    align-items: flex-start;
    gap: 0;
    transition: right var(--transition);
    z-index: 90;
    border-left: 1px solid var(--border);
  }

  .nav.open { right: 0; }

  .nav ul { flex-direction: column; gap: 0; width: 100%; }

  .nav a {
    display: block;
    padding: 1rem 0;
    font-size: 1rem;
    border-bottom: 1px solid var(--border);
  }

  .nav a::after { display: none; }

  .nav-cta { margin-top: 2rem; width: 100%; justify-content: center; }
}
</style>
