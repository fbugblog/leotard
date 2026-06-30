<script setup>
const navLinks = [
  { href: '#concept',  label: 'コンセプト' },
  { href: '#programs', label: 'クラス紹介' },
  { href: '#features', label: 'GRACEの特徴' },
  { href: '#contact',  label: 'お問い合わせ' },
]

function smooth(e, href) {
  e.preventDefault()
  document.querySelector(href)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}

function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>

<template>
  <footer class="footer">
    <div class="container">
      <div class="top">
        <div class="brand">
          <a href="#" class="logo" @click.prevent="scrollToTop" aria-label="GRACE STUDIOトップへ">
            <span class="logo-mark" aria-hidden="true">G</span>
            <div class="logo-text">
              <span class="logo-name">GRACE</span>
              <span class="logo-sub">STUDIO</span>
            </div>
          </a>
          <p class="brand-tagline">美しい動きが、あなたを変える。</p>
        </div>

        <nav class="footer-nav" aria-label="フッターナビゲーション">
          <p class="nav-heading">ページ</p>
          <ul>
            <li v-for="link in navLinks" :key="link.label">
              <a :href="link.href" @click="(e) => smooth(e, link.href)">{{ link.label }}</a>
            </li>
          </ul>
        </nav>
      </div>

      <div class="bottom">
        <p class="copyright">&copy; 2024 GRACE STUDIO. All rights reserved.</p>
        <p class="bottom-note">新体操 · ボディメイキング専門スタジオ</p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: var(--charcoal);
  padding-block: 4.5rem 2rem;
}

.top {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 4rem;
  margin-bottom: 4rem;
  padding-bottom: 3rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.07);
  flex-wrap: wrap;
}

/* Logo */
.logo {
  display: inline-flex;
  align-items: center;
  gap: 0.7rem;
  margin-bottom: 1rem;
  transition: opacity var(--transition);
}

.logo:hover { opacity: 0.75; }

.logo-mark {
  width: 40px; height: 40px;
  border-radius: 10px;
  background: var(--pink);
  color: var(--surface);
  font-family: var(--font-display);
  font-size: 1.1rem;
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
}

.logo-text {
  display: flex;
  flex-direction: column;
  line-height: 1;
  gap: 0.12em;
}

.logo-name {
  font-family: var(--font-display);
  font-size: 0.95rem;
  font-weight: 700;
  letter-spacing: 0.18em;
  color: var(--surface);
}

.logo-sub {
  font-family: var(--font-display);
  font-size: 0.58rem;
  font-weight: 400;
  letter-spacing: 0.22em;
  color: rgba(255, 255, 255, 0.35);
}

.brand-tagline {
  font-family: var(--font-serif);
  font-style: italic;
  font-size: 0.88rem;
  color: rgba(255, 255, 255, 0.3);
}

/* Footer nav */
.nav-heading {
  font-family: var(--font-display);
  font-size: 0.58rem;
  font-weight: 700;
  letter-spacing: 0.28em;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.22);
  margin-bottom: 1rem;
}

.footer-nav ul {
  display: flex;
  flex-direction: column;
  gap: 0.55rem;
}

.footer-nav a {
  font-size: 0.82rem;
  color: rgba(255, 255, 255, 0.4);
  transition: color var(--transition);
}

.footer-nav a:hover { color: var(--pink-200); }

/* Bottom */
.bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.copyright {
  font-family: var(--font-display);
  font-size: 0.7rem;
  color: rgba(255, 255, 255, 0.18);
}

.bottom-note {
  font-family: var(--font-display);
  font-size: 0.62rem;
  letter-spacing: 0.14em;
  color: rgba(255, 255, 255, 0.13);
}

@media (max-width: 600px) {
  .top { flex-direction: column; gap: 2.5rem; }
  .bottom { flex-direction: column; align-items: flex-start; gap: 0.3rem; }
}
</style>
