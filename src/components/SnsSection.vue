<script setup>
const INSTAGRAM_URL = 'https://www.instagram.com/juneberry_leotard/'
const LINE_URL = null  // アカウント未作成 → null の間は Coming Soon 表示
</script>

<template>
  <section id="sns" class="sns section">
    <div class="container">
      <span class="eyebrow center" style="color: var(--dark); opacity:.5">Follow Us</span>
      <h2 class="display-title center">SNS で最新情報をチェック</h2>
      <p class="sub center">
        新作・期間限定カラー・大会情報・コーディネートを毎日発信中。<br>
        フォローしてJune BERRYをもっと楽しんでください。
      </p>

      <div class="cards">
        <!-- Instagram -->
        <a
          :href="INSTAGRAM_URL"
          class="card card--instagram"
          target="_blank"
          rel="noopener noreferrer"
        >
          <div class="card__icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" aria-hidden="true">
              <rect x="2" y="2" width="20" height="20" rx="5" ry="5"/>
              <circle cx="12" cy="12" r="4"/>
              <circle cx="17.5" cy="6.5" r="0.5" fill="currentColor" stroke="none"/>
            </svg>
          </div>
          <div class="card__text">
            <span class="card__platform">Instagram</span>
            <span class="card__handle">@juneberry_leotard</span>
            <span class="card__action">フォローする →</span>
          </div>
          <div class="card__gradient" aria-hidden="true" />
        </a>

        <!-- LINE -->
        <div
          class="card card--line"
          :class="{ 'card--coming-soon': !LINE_URL }"
        >
          <div class="card__icon">
            <svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
              <path d="M19.365 9.89c.50 0 .91.41.91.91s-.41.91-.91.91h-2.27v1.37h2.27c.50 0 .91.41.91.91s-.41.91-.91.91h-3.18c-.50 0-.91-.41-.91-.91V9.89c0-.50.41-.91.91-.91h3.18zm-12.73.91c0-.50-.41-.91-.91-.91s-.91.41-.91.91v3.64c0 .50.41.91.91.91s.91-.41.91-.91V10.8zm1.82-.91c-.50 0-.91.41-.91.91v3.64c0 .50.41.91.91.91h3.18c.50 0 .91-.41.91-.91s-.41-.91-.91-.91H9.35V10.8c0-.50-.41-.91-.91-.91zm3.18 0c-.50 0-.91.41-.91.91v3.64c0 .50.41.91.91.91s.91-.41.91-.91v-1.37l1.58 1.96c.18.22.44.32.70.32.50 0 .91-.41.91-.91V10.8c0-.50-.41-.91-.91-.91s-.91.41-.91.91v1.37l-1.58-1.96c-.17-.22-.44-.32-.70-.32zM12 2C6.48 2 2 6.03 2 11c0 3.28 1.81 6.16 4.55 7.89-.15.54-.56 2.03-.64 2.34-.10.37.14.37.30.27.12-.07 2.01-1.32 2.82-1.86.62.09 1.26.14 1.92.14 5.52 0 10-4.03 10-9 0-4.97-4.48-9-10-9z"/>
            </svg>
          </div>
          <div class="card__text">
            <span class="card__platform">LINE 公式</span>
            <span class="card__handle" v-if="LINE_URL">@juneberry</span>
            <span class="card__handle coming-soon" v-else">近日公開予定</span>
            <span class="card__action" v-if="LINE_URL">友だち追加 →</span>
            <span class="card__action coming-label" v-else>Coming Soon</span>
          </div>
          <div class="card__gradient" aria-hidden="true" />
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.sns {
  background: var(--cream);
  border-top: 1px solid rgba(7,4,14,0.06);
}

.sub {
  color: var(--text-muted-dark);
  max-width: 46ch;
  margin-inline: auto;
  margin-top: 1rem;
  margin-bottom: 3.5rem;
  line-height: 2;
}

.cards {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
  max-width: 760px;
  margin-inline: auto;
}

/* Card base */
.card {
  position: relative;
  display: flex;
  align-items: center;
  gap: 1.5rem;
  padding: 2.2rem 2rem;
  border-radius: var(--radius);
  overflow: hidden;
  text-decoration: none;
  transition: transform var(--transition), box-shadow var(--transition);
  cursor: pointer;
}

.card:not(.card--coming-soon):hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
}

.card--coming-soon { cursor: default; opacity: 0.65; }

/* Instagram */
.card--instagram {
  background: linear-gradient(135deg, #833ab4 0%, #c2547a 50%, #E1306C 100%);
  color: var(--white);
}

/* LINE */
.card--line {
  background: #06C755;
  color: var(--white);
}

/* Icon */
.card__icon {
  flex-shrink: 0;
  width: 52px; height: 52px;
  background: rgba(255,255,255,0.18);
  border-radius: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.card__icon svg {
  width: 26px; height: 26px;
  color: var(--white);
}

/* Text */
.card__text {
  display: flex;
  flex-direction: column;
  gap: 0.2rem;
  position: relative;
  z-index: 1;
}

.card__platform {
  font-size: 0.68rem;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.7);
}

.card__handle {
  font-family: var(--font-serif);
  font-size: 1.2rem;
  font-weight: 600;
  color: var(--white);
}

.card__handle.coming-soon {
  font-family: var(--font-sans);
  font-size: 0.9rem;
  font-weight: 400;
  opacity: 0.8;
}

.card__action {
  font-size: 0.78rem;
  color: rgba(255,255,255,0.75);
  margin-top: 0.2rem;
}

.card__action.coming-label {
  font-size: 0.68rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  background: rgba(255,255,255,0.2);
  padding: 0.2em 0.7em;
  border-radius: 50px;
  color: rgba(255,255,255,0.9);
  display: inline-block;
  width: fit-content;
}

/* Gradient overlay */
.card__gradient {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 80% 50%, rgba(255,255,255,0.1), transparent 60%);
  pointer-events: none;
}

@media (max-width: 600px) {
  .cards { grid-template-columns: 1fr; }
}
</style>
