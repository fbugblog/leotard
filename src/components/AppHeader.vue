<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const scrolled = ref(false)
const menuOpen = ref(false)

const navLinks = [
  { href: '#concept',      label: 'コンセプト' },
  { href: '#products',     label: 'コレクション' },
  { href: '#features',     label: '特徴' },
  { href: '#sns',          label: 'SNS' },
  { href: '#contact',      label: 'お問い合わせ' },
]

function handleScroll() { scrolled.value = window.scrollY > 60 }
function toggleMenu() { menuOpen.value = !menuOpen.value }
function closeMenu() { menuOpen.value = false }

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
      <a href="#" class="logo" @click.prevent="window.scrollTo({ top: 0, behavior: 'smooth' })">
        <span class="june">June</span>
        <span class="berry">BERRY</span>
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
  padding: 1.4rem 0;
  transition: background var(--transition), box-shadow var(--transition), padding var(--transition);
}

.header.scrolled {
  background: rgba(7, 4, 14, 0.92);
  backdrop-filter: blur(16px);
  box-shadow: 0 1px 0 rgba(255,255,255,0.06);
  padding: 0.9rem 0;
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
  font-style: italic;
  font-size: 1.45rem;
  font-weight: 300;
  color: var(--champagne);
}

.berry {
  font-family: var(--font-serif);
  font-size: 1.2rem;
  font-weight: 600;
  letter-spacing: 0.14em;
  color: var(--gold);
}

/* Nav */
.nav ul { display: flex; gap: 2.2rem; }

.nav a {
  font-size: 0.78rem;
  letter-spacing: 0.1em;
  color: rgba(255,255,255,0.7);
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
  background: var(--champagne);
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
  background: rgba(7, 4, 14, 0.6);
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
    background: var(--dark-2);
    padding: 6rem 2rem 2rem;
    transition: right var(--transition);
    z-index: 90;
    border-left: 1px solid rgba(255,255,255,0.06);
  }

  .nav.open { right: 0; }

  .nav ul { flex-direction: column; gap: 0; }

  .nav a {
    display: block;
    padding: 1.1rem 0;
    font-size: 1rem;
    border-bottom: 1px solid rgba(255,255,255,0.06);
    color: var(--text-light);
  }

  .nav a::after { display: none; }
}
</style>
