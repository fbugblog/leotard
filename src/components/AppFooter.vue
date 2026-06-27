<script setup>
const navLinks = [
  { href: '#story',   label: '想い' },
  { href: '#gallery', label: 'メニュー' },
  { href: '#pricing', label: '料金' },
  { href: '#process', label: '流れ' },
  { href: '#faq',     label: 'FAQ' },
  { href: '#contact', label: 'お問い合わせ' },
]

const legalLinks = [
  { href: '#', label: '特定商取引法に基づく表記' },
  { href: '#', label: 'プライバシーポリシー' },
  { href: '#', label: '返品・交換について' },
  { href: '#', label: 'サイズガイド' },
]

const INSTAGRAM_URL = 'https://www.instagram.com/juneberry_leotard/'

function smooth(e, href) {
  e.preventDefault()
  document.querySelector(href)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}
</script>

<template>
  <footer class="footer">
    <div class="container">
      <div class="top">
        <!-- Brand -->
        <div class="brand">
          <p class="logo">
            <span class="june">June</span>
            <span class="berry">BERRY</span>
          </p>
          <p class="tagline">演技に魂を宿す、一枚。</p>
          <p class="sport">新体操専用レオタード</p>

          <!-- Social icons -->
          <div class="socials">
            <a :href="INSTAGRAM_URL" target="_blank" rel="noopener noreferrer" aria-label="Instagram" class="social-icon">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                <rect x="2" y="2" width="20" height="20" rx="5" ry="5"/>
                <circle cx="12" cy="12" r="4"/>
                <circle cx="17.5" cy="6.5" r="0.5" fill="currentColor" stroke="none"/>
              </svg>
            </a>
            <span class="social-icon social-icon--disabled" aria-label="LINE（準備中）" title="LINE公式アカウント準備中">
              <svg viewBox="0 0 24 24" fill="currentColor">
                <path d="M19.365 9.89c.50 0 .91.41.91.91s-.41.91-.91.91h-2.27v1.37h2.27c.50 0 .91.41.91.91s-.41.91-.91.91h-3.18c-.50 0-.91-.41-.91-.91V9.89c0-.50.41-.91.91-.91h3.18zm-12.73.91c0-.50-.41-.91-.91-.91s-.91.41-.91.91v3.64c0 .50.41.91.91.91s.91-.41.91-.91V10.8zm1.82-.91c-.50 0-.91.41-.91.91v3.64c0 .50.41.91.91.91h3.18c.50 0 .91-.41.91-.91s-.41-.91-.91-.91H9.35V10.8c0-.50-.41-.91-.91-.91zm3.18 0c-.50 0-.91.41-.91.91v3.64c0 .50.41.91.91.91s.91-.41.91-.91v-1.37l1.58 1.96c.18.22.44.32.70.32.50 0 .91-.41.91-.91V10.8c0-.50-.41-.91-.91-.91s-.91.41-.91.91v1.37l-1.58-1.96c-.17-.22-.44-.32-.70-.32zM12 2C6.48 2 2 6.03 2 11c0 3.28 1.81 6.16 4.55 7.89-.15.54-.56 2.03-.64 2.34-.10.37.14.37.30.27.12-.07 2.01-1.32 2.82-1.86.62.09 1.26.14 1.92.14 5.52 0 10-4.03 10-9 0-4.97-4.48-9-10-9z"/>
              </svg>
              <span class="coming-badge">準備中</span>
            </span>
          </div>
        </div>

        <!-- Nav links -->
        <nav class="nav" aria-label="フッターナビゲーション">
          <div class="nav-col">
            <p class="nav-heading">ページ</p>
            <ul>
              <li v-for="link in navLinks" :key="link.label">
                <a :href="link.href" @click="(e) => smooth(e, link.href)">{{ link.label }}</a>
              </li>
            </ul>
          </div>
          <div class="nav-col">
            <p class="nav-heading">ポリシー</p>
            <ul>
              <li v-for="link in legalLinks" :key="link.label">
                <a :href="link.href">{{ link.label }}</a>
              </li>
            </ul>
          </div>
        </nav>
      </div>

      <div class="bottom">
        <p>&copy; 2024 June BERRY. All rights reserved.</p>
        <p class="bottom-sport">新体操専用レオタード専門店</p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: #1E0812;
  border-top: 1px solid rgba(191,78,120,0.12);
  padding-block: 4rem 2rem;
}

.top {
  display: flex;
  justify-content: space-between;
  gap: 4rem;
  margin-bottom: 3rem;
  flex-wrap: wrap;
}

/* Brand */
.brand { max-width: 300px; }

.logo {
  display: flex;
  align-items: baseline;
  gap: 0.2em;
  margin-bottom: 0.5rem;
}

.june {
  font-family: var(--font-serif);
  font-style: italic;
  font-size: 1.8rem;
  font-weight: 300;
  color: var(--champagne);
}

.berry {
  font-family: var(--font-serif);
  font-size: 1.5rem;
  font-weight: 600;
  letter-spacing: 0.14em;
  color: var(--gold);
}

.tagline {
  font-family: var(--font-serif);
  font-style: italic;
  font-size: 0.9rem;
  color: rgba(255,255,255,0.35);
  margin-bottom: 0.3rem;
}

.sport {
  font-size: 0.68rem;
  letter-spacing: 0.15em;
  color: rgba(255,255,255,0.2);
  text-transform: uppercase;
  margin-bottom: 1.8rem;
}

/* Socials */
.socials {
  display: flex;
  gap: 0.8rem;
}

.social-icon {
  position: relative;
  width: 40px; height: 40px;
  border: 1px solid rgba(255,255,255,0.15);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: rgba(255,255,255,0.5);
  transition: color var(--transition), border-color var(--transition), background var(--transition);
  cursor: pointer;
}

.social-icon:not(.social-icon--disabled):hover {
  color: var(--gold);
  border-color: var(--gold);
  background: rgba(191,78,120,0.1);
}

.social-icon--disabled { opacity: 0.35; cursor: default; }

.social-icon svg { width: 18px; height: 18px; }

.coming-badge {
  position: absolute;
  top: -6px; right: -6px;
  background: var(--gold);
  color: var(--dark);
  font-size: 0.5rem;
  font-weight: 600;
  padding: 0.15em 0.4em;
  border-radius: 4px;
  letter-spacing: 0;
  white-space: nowrap;
}

/* Nav */
.nav {
  display: flex;
  gap: 4rem;
}

.nav-col { display: flex; flex-direction: column; gap: 1rem; }

.nav-heading {
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.3);
}

.nav ul { display: flex; flex-direction: column; gap: 0.5rem; }

.nav a {
  font-size: 0.82rem;
  color: rgba(255,255,255,0.5);
  transition: color var(--transition);
}

.nav a:hover { color: var(--gold); }

/* Bottom */
.bottom {
  border-top: 1px solid rgba(255,255,255,0.06);
  padding-top: 1.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.bottom p {
  font-size: 0.72rem;
  color: rgba(255,255,255,0.25);
}

@media (max-width: 768px) {
  .top { flex-direction: column; gap: 2.5rem; }
  .nav { gap: 2rem; }
  .bottom { flex-direction: column; align-items: flex-start; }
}
</style>
