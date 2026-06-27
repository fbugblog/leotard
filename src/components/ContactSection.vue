<script setup>
import { ref } from 'vue'

const email = ref('')
const submitted = ref(false)

function handleSubmit() {
  if (!email.value) return
  submitted.value = true
}
</script>

<template>
  <section id="contact" class="contact section">
    <div class="container">
      <div class="inner">
        <div class="left">
          <span class="eyebrow">Newsletter</span>
          <h2 class="display-title">最新情報を<br>いち早くお届け</h2>
          <p>
            新コレクション・大会シーズン限定カラー・キャンペーン情報を
            メールでお届けします。登録は無料、いつでも解除できます。
          </p>

          <div class="contact-info">
            <div class="info-row">
              <span>📧</span>
              <span>info@juneberry.jp</span>
            </div>
            <div class="info-row">
              <span>🕐</span>
              <span>平日 10:00〜18:00</span>
            </div>
          </div>
        </div>

        <div class="right">
          <Transition name="fade" mode="out-in">
            <form v-if="!submitted" @submit.prevent="handleSubmit" novalidate>
              <label class="sr-only" for="email">メールアドレス</label>
              <input
                id="email"
                v-model="email"
                type="email"
                placeholder="your@email.com"
                required
              />
              <button type="submit" class="btn btn-gold">メルマガ登録</button>
              <p class="note">プライバシーポリシーに同意の上でご登録ください。</p>
            </form>

            <div v-else class="success" role="status">
              <div class="success-icon">✓</div>
              <p>ご登録ありがとうございます！<br>素敵な情報をお届けします。</p>
            </div>
          </Transition>
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
  background: linear-gradient(to right, transparent, rgba(191, 78, 120, 0.4), transparent);
}

.inner {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 6rem;
  align-items: center;
}

/* Left */
.eyebrow { color: var(--gold); }

.display-title {
  color: var(--champagne);
  margin: 0.5rem 0 1.2rem;
}

.left p {
  color: rgba(255,255,255,0.5);
  line-height: 1.9;
  font-size: 0.9rem;
}

.contact-info {
  margin-top: 2.5rem;
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.info-row {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  font-size: 0.85rem;
  color: rgba(255,255,255,0.5);
}

/* Right / Form */
form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

input {
  width: 100%;
  padding: 1em 1.4em;
  background: rgba(255,255,255,0.06);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 50px;
  font-family: var(--font-sans);
  font-size: 0.9rem;
  color: var(--white);
  outline: none;
  transition: border-color var(--transition), background var(--transition);
}

input::placeholder { color: rgba(255,255,255,0.3); }

input:focus {
  border-color: var(--gold);
  background: rgba(255,255,255,0.09);
}

.btn { width: 100%; justify-content: center; }

.note {
  font-size: 0.72rem;
  color: rgba(255,255,255,0.3);
  text-align: center;
}

/* Success */
.success {
  text-align: center;
  padding: 3rem 2rem;
  border: 1px solid rgba(201, 162, 39, 0.3);
  border-radius: var(--radius);
}

.success-icon {
  width: 52px; height: 52px;
  border-radius: 50%;
  background: var(--gold);
  color: var(--dark);
  font-size: 1.4rem;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1rem;
  font-weight: 700;
}

.success p {
  color: var(--champagne);
  line-height: 1.8;
}

/* Transition */
.fade-enter-active, .fade-leave-active { transition: opacity 0.4s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; }

@media (max-width: 768px) {
  .inner { grid-template-columns: 1fr; gap: 3rem; }
}
</style>
