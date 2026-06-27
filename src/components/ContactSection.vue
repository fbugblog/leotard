<script setup>
import { ref } from 'vue'

const INSTAGRAM_URL = 'https://www.instagram.com/juneberry_leotard/'

const email = ref('')
const message = ref('')
const submitted = ref(false)

function handleSubmit() {
  if (!email.value) return
  submitted.value = true
}
</script>

<template>
  <section id="contact" class="contact section">
    <div class="container">
      <div class="header">
        <span class="eyebrow">Contact</span>
        <h2 class="display-title">お問い合わせ・ご相談</h2>
        <p class="header-sub">
          相談・お見積りは無料です。まずはお気軽にご連絡ください。
        </p>
      </div>

      <!-- Primary CTAs -->
      <div class="cta-cards">
        <a :href="INSTAGRAM_URL" target="_blank" rel="noopener noreferrer" class="cta-card cta-card--instagram">
          <div class="cta-card__icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" aria-hidden="true">
              <rect x="2" y="2" width="20" height="20" rx="5" ry="5"/>
              <circle cx="12" cy="12" r="4"/>
              <circle cx="17.5" cy="6.5" r="0.5" fill="currentColor" stroke="none"/>
            </svg>
          </div>
          <div class="cta-card__body">
            <span class="cta-card__label">最も簡単・すぐ繋がれる</span>
            <strong class="cta-card__title">Instagramで相談する</strong>
            <span class="cta-card__handle">@juneberry_leotard</span>
          </div>
          <span class="cta-card__arrow">→</span>
        </a>

        <div class="cta-card cta-card--line cta-card--disabled" title="LINE公式アカウント準備中">
          <div class="cta-card__icon">
            <svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
              <path d="M12 2C6.48 2 2 6.03 2 11c0 3.28 1.81 6.16 4.55 7.89-.15.54-.56 2.03-.64 2.34-.10.37.14.37.30.27.12-.07 2.01-1.32 2.82-1.86.62.09 1.26.14 1.92.14 5.52 0 10-4.03 10-9 0-4.97-4.48-9-10-9z"/>
            </svg>
          </div>
          <div class="cta-card__body">
            <span class="cta-card__label">準備中</span>
            <strong class="cta-card__title">LINEで相談する</strong>
            <span class="cta-card__handle">近日公開予定</span>
          </div>
          <span class="coming">Coming Soon</span>
        </div>
      </div>

      <!-- Form -->
      <div class="form-block">
        <h3 class="form-title">メールでお問い合わせ</h3>
        <Transition name="fade" mode="out-in">
          <form v-if="!submitted" @submit.prevent="handleSubmit" novalidate>
            <div class="form-row">
              <div class="form-group">
                <label for="email">メールアドレス <span class="required">必須</span></label>
                <input id="email" v-model="email" type="email" placeholder="your@email.com" required />
              </div>
            </div>
            <div class="form-group">
              <label for="message">お問い合わせ内容</label>
              <textarea id="message" v-model="message" rows="4" placeholder="ご相談内容をご記入ください（制作メニュー・イメージ・大会日程など）" />
            </div>
            <button type="submit" class="btn btn-gold submit-btn">送信する</button>
            <p class="note">プライバシーポリシーに同意の上でご送信ください。通常1〜2営業日以内にご返信します。</p>
          </form>

          <div v-else class="success" role="status">
            <div class="success-icon">✓</div>
            <p>ご連絡ありがとうございます！<br>1〜2営業日以内にご返信します。</p>
          </div>
        </Transition>
      </div>

      <!-- Info row -->
      <div class="info-row">
        <div class="info-item">
          <span class="info-icon">📧</span>
          <div>
            <span class="info-label">メール</span>
            <span class="info-value">info@juneberry.jp</span>
          </div>
        </div>
        <div class="info-item">
          <span class="info-icon">🕐</span>
          <div>
            <span class="info-label">対応時間</span>
            <span class="info-value">平日 10:00〜18:00</span>
          </div>
        </div>
        <div class="info-item">
          <span class="info-icon">📦</span>
          <div>
            <span class="info-label">配送</span>
            <span class="info-value">全国送料無料</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact {
  background: var(--dark-2);
  position: relative;
}

.contact::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 1px;
  background: linear-gradient(to right, transparent, rgba(191,78,120,0.4), transparent);
}

.header {
  margin-bottom: 3rem;
}

.header .display-title { color: var(--champagne); margin: 0.5rem 0 0; }

.header-sub {
  margin-top: 0.8rem;
  font-size: 0.9rem;
  color: rgba(255,255,255,0.45);
  line-height: 1.8;
}

/* CTA cards */
.cta-cards {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  margin-bottom: 3rem;
}

.cta-card {
  display: flex;
  align-items: center;
  gap: 1.2rem;
  padding: 1.5rem 2rem;
  border-radius: var(--radius);
  text-decoration: none;
  transition: transform var(--transition), box-shadow var(--transition);
  cursor: pointer;
  position: relative;
}

.cta-card:not(.cta-card--disabled):hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-md);
}

.cta-card--instagram {
  background: linear-gradient(135deg, #833ab4 0%, #c2547a 50%, #E1306C 100%);
  color: var(--white);
}

.cta-card--line {
  background: #06C755;
  color: var(--white);
}

.cta-card--disabled { opacity: 0.5; cursor: default; }

.cta-card__icon {
  width: 48px; height: 48px;
  background: rgba(255,255,255,0.2);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.cta-card__icon svg { width: 22px; height: 22px; }

.cta-card__body {
  display: flex;
  flex-direction: column;
  gap: 0.1rem;
  flex: 1;
}

.cta-card__label {
  font-size: 0.65rem;
  letter-spacing: 0.1em;
  color: rgba(255,255,255,0.7);
}

.cta-card__title {
  font-size: 1rem;
  font-weight: 600;
  color: var(--white);
}

.cta-card__handle {
  font-size: 0.75rem;
  color: rgba(255,255,255,0.7);
}

.cta-card__arrow {
  font-size: 1.2rem;
  color: rgba(255,255,255,0.7);
  flex-shrink: 0;
}

.coming {
  position: absolute;
  top: 0.7rem; right: 0.7rem;
  background: rgba(0,0,0,0.25);
  color: var(--white);
  font-size: 0.55rem;
  font-weight: 600;
  letter-spacing: 0.1em;
  padding: 0.2em 0.6em;
  border-radius: 4px;
}

/* Form */
.form-block {
  background: rgba(255,255,255,0.04);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: var(--radius);
  padding: 2.5rem;
  margin-bottom: 2.5rem;
}

.form-title {
  font-family: var(--font-serif);
  font-size: 1.1rem;
  font-weight: 600;
  color: var(--champagne);
  margin-bottom: 1.8rem;
}

.form-row { display: grid; grid-template-columns: 1fr; gap: 1rem; }

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.form-group label {
  font-size: 0.8rem;
  color: rgba(255,255,255,0.5);
  letter-spacing: 0.05em;
}

.required {
  font-size: 0.65rem;
  color: var(--gold);
  margin-left: 0.3em;
  background: rgba(191,78,120,0.15);
  padding: 0.1em 0.4em;
  border-radius: 4px;
}

input, textarea {
  width: 100%;
  padding: 0.9em 1.2em;
  background: rgba(255,255,255,0.06);
  border: 1px solid rgba(255,255,255,0.1);
  border-radius: 10px;
  font-family: var(--font-sans);
  font-size: 0.9rem;
  color: var(--white);
  outline: none;
  transition: border-color var(--transition), background var(--transition);
  resize: vertical;
}

input::placeholder, textarea::placeholder { color: rgba(255,255,255,0.25); }

input:focus, textarea:focus {
  border-color: var(--gold);
  background: rgba(255,255,255,0.09);
}

.submit-btn { margin-top: 0.5rem; }

.note {
  margin-top: 0.8rem;
  font-size: 0.72rem;
  color: rgba(255,255,255,0.3);
}

/* Success */
.success {
  text-align: center;
  padding: 3rem 2rem;
}

.success-icon {
  width: 52px; height: 52px;
  border-radius: 50%;
  background: var(--gold);
  color: var(--dark);
  font-size: 1.4rem;
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1rem;
}

.success p { color: var(--champagne); line-height: 1.8; }

/* Info row */
.info-row {
  display: flex;
  gap: 2.5rem;
  flex-wrap: wrap;
}

.info-item {
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.info-icon { font-size: 1.2rem; }

.info-item > div {
  display: flex;
  flex-direction: column;
  gap: 0.1rem;
}

.info-label {
  font-size: 0.65rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.3);
}

.info-value {
  font-size: 0.85rem;
  color: rgba(255,255,255,0.6);
}

/* Transition */
.fade-enter-active, .fade-leave-active { transition: opacity 0.4s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; }

@media (max-width: 768px) {
  .cta-cards { grid-template-columns: 1fr; }
  .form-block { padding: 1.5rem; }
  .info-row { gap: 1.5rem; }
}
</style>
