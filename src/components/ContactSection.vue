<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)
const fname = ref('')
const email = ref('')
const message = ref('')
const submitted = ref(false)

function handleSubmit() {
  if (!email.value || !fname.value) return
  submitted.value = true
}

const info = [
  { label: '営業時間', value: '平日 10:00〜20:00 / 土日祝 9:00〜18:00' },
  { label: '体験レッスン', value: '随時受付中（完全予約制）' },
  { label: '所在地', value: '〒XXX-XXXX 東京都○○区○○1-2-3' },
]

onMounted(() => {
  const obs = new IntersectionObserver(
    es => es.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); obs.unobserve(e.target) } }),
    { threshold: 0.1 }
  )
  sectionRef.value?.querySelectorAll('.scroll-in').forEach(el => obs.observe(el))
})
</script>

<template>
  <section id="contact" class="contact" ref="sectionRef">

    <!-- CTA band -->
    <div class="cta-band">
      <div class="container">
        <div class="cta-inner scroll-in">
          <div class="cta-content">
            <span class="eyebrow" style="color:rgba(255,255,255,0.55)">TRIAL LESSON</span>
            <h2 class="cta-title">
              体験レッスン、<br>
              受付中です。
            </h2>
            <p class="cta-sub">
              まずは気軽に体験してみてください。<br>
              初めての方も、経験者の方も大歓迎です。
            </p>
          </div>
          <div class="cta-visual" aria-hidden="true">
            <div class="cta-ring cta-ring-1" />
            <div class="cta-ring cta-ring-2" />
            <span class="cta-g">G</span>
          </div>
        </div>
      </div>
    </div>

    <!-- Form section -->
    <div class="form-section section">
      <div class="container">
        <div class="form-grid">

          <!-- Info column -->
          <div class="info-col scroll-in">
            <span class="eyebrow">CONTACT</span>
            <h3 class="info-title">お問い合わせ</h3>
            <p class="info-sub">
              ご不明な点・体験レッスンのご予約など、<br>
              お気軽にご連絡ください。
            </p>

            <dl class="info-list">
              <div v-for="item in info" :key="item.label" class="info-item">
                <dt class="info-label">{{ item.label }}</dt>
                <dd class="info-value">{{ item.value }}</dd>
              </div>
            </dl>
          </div>

          <!-- Form column -->
          <div class="form-col scroll-in" style="transition-delay:.1s">
            <Transition name="fade" mode="out-in">
              <form v-if="!submitted" @submit.prevent="handleSubmit" novalidate class="form">
                <div class="field">
                  <label for="fname">お名前 <span class="req" aria-label="必須">*</span></label>
                  <input id="fname" v-model="fname" type="text" placeholder="山田 花子" required autocomplete="name" />
                </div>
                <div class="field">
                  <label for="email">メールアドレス <span class="req" aria-label="必須">*</span></label>
                  <input id="email" v-model="email" type="email" placeholder="your@email.com" required autocomplete="email" />
                </div>
                <div class="field">
                  <label for="message">お問い合わせ内容</label>
                  <textarea id="message" v-model="message" rows="4" placeholder="体験レッスンを希望するクラス、ご質問など" />
                </div>
                <button type="submit" class="btn btn-primary submit-btn">
                  送信する
                  <svg width="16" height="16" viewBox="0 0 16 16" fill="none" aria-hidden="true">
                    <path d="M3 8h10M9 4l4 4-4 4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
                  </svg>
                </button>
                <p class="form-note">通常1〜2営業日以内にご返信いたします。</p>
              </form>

              <div v-else class="success" role="status">
                <div class="success-mark" aria-hidden="true">✓</div>
                <p class="success-msg">
                  送信ありがとうございます！<br>
                  1〜2営業日以内にご連絡いたします。
                </p>
              </div>
            </Transition>
          </div>

        </div>
      </div>
    </div>

  </section>
</template>

<style scoped>
/* CTA band */
.cta-band {
  background: linear-gradient(135deg, var(--pink-700) 0%, var(--pink) 55%, var(--violet) 100%);
  padding-block: 6rem;
  position: relative;
  overflow: hidden;
}

.cta-inner {
  display: grid;
  grid-template-columns: 1fr auto;
  align-items: center;
  gap: 5rem;
}

.cta-title {
  font-family: var(--font-serif);
  font-size: clamp(2.2rem, 5vw, 3.8rem);
  font-weight: 400;
  color: var(--surface);
  line-height: 1.2;
  margin-block: 0.8rem 1.1rem;
}

.cta-sub {
  font-size: 0.95rem;
  color: rgba(255, 255, 255, 0.72);
  line-height: 2;
}

/* CTA visual */
.cta-visual {
  position: relative;
  width: 180px; height: 180px;
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.cta-ring {
  position: absolute;
  border-radius: 50%;
  border: 1.5px solid rgba(255, 255, 255, 0.2);
}

.cta-ring-1 { inset: 0; }
.cta-ring-2 { inset: 24px; animation: spin-cw 12s linear infinite; }

@keyframes spin-cw { from { transform: rotate(0); } to { transform: rotate(360deg); } }

.cta-g {
  font-family: var(--font-display);
  font-size: 4.5rem;
  font-weight: 700;
  color: rgba(255, 255, 255, 0.3);
  line-height: 1;
}

/* Form section */
.form-section {
  background: var(--body-bg);
}

.form-grid {
  display: grid;
  grid-template-columns: 1fr 1.6fr;
  gap: 6rem;
  align-items: start;
}

/* Info col */
.info-title {
  font-family: var(--font-serif);
  font-size: 1.9rem;
  font-weight: 400;
  color: var(--text);
  margin: 0.5rem 0 0.8rem;
}

.info-sub {
  font-size: 0.88rem;
  color: var(--text-muted);
  line-height: 1.9;
  margin-bottom: 2.5rem;
}

.info-list {
  display: flex;
  flex-direction: column;
  gap: 0;
}

.info-item {
  padding-block: 1.1rem;
  border-bottom: 1px solid var(--border);
}

.info-label {
  font-family: var(--font-display);
  font-size: 0.6rem;
  font-weight: 700;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--pink);
  margin-bottom: 0.3rem;
  display: block;
}

.info-value {
  font-size: 0.88rem;
  color: var(--text-mid);
  line-height: 1.7;
  display: block;
}

/* Form */
.form {
  background: var(--surface);
  border-radius: var(--radius-lg);
  padding: 2.5rem;
  border: 1.5px solid var(--border);
  display: flex;
  flex-direction: column;
  gap: 1.3rem;
  box-shadow: var(--shadow-sm);
}

.field {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.field label {
  font-family: var(--font-display);
  font-size: 0.73rem;
  font-weight: 500;
  letter-spacing: 0.04em;
  color: var(--text-mid);
}

.req { color: var(--pink); margin-left: 0.15em; }

input, textarea {
  width: 100%;
  padding: 0.85em 1.1em;
  background: var(--body-bg);
  border: 1.5px solid var(--border);
  border-radius: var(--radius-sm);
  font-family: var(--font-sans);
  font-size: 0.88rem;
  color: var(--text);
  outline: none;
  transition: border-color var(--transition), background var(--transition), box-shadow var(--transition);
  resize: vertical;
}

input::placeholder, textarea::placeholder { color: var(--text-muted); }

input:focus, textarea:focus {
  border-color: var(--pink);
  background: var(--surface);
  box-shadow: 0 0 0 3px rgba(240, 78, 132, 0.1);
}

.submit-btn { align-self: flex-start; }

.form-note {
  font-size: 0.72rem;
  color: var(--text-muted);
  margin-top: -0.4rem;
}

/* Success */
.success {
  background: var(--surface);
  border-radius: var(--radius-lg);
  padding: 4rem 2.5rem;
  border: 1.5px solid var(--border);
  text-align: center;
  box-shadow: var(--shadow-sm);
}

.success-mark {
  width: 56px; height: 56px;
  border-radius: 50%;
  background: var(--pink);
  color: var(--surface);
  font-size: 1.4rem;
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1.2rem;
}

.success-msg {
  font-size: 0.95rem;
  color: var(--text-mid);
  line-height: 2;
}

/* Transitions */
.fade-enter-active, .fade-leave-active { transition: opacity 0.4s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; }

/* Responsive */
@media (max-width: 1000px) {
  .cta-inner { grid-template-columns: 1fr; }
  .cta-visual { display: none; }
  .form-grid { grid-template-columns: 1fr; gap: 3rem; }
}

@media (max-width: 600px) {
  .form { padding: 1.5rem; }
  .cta-band { padding-block: 4rem; }
}
</style>
