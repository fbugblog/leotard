<script setup>
import { ref } from 'vue'

const email = ref('')
const submitted = ref(false)

const contactInfo = [
  { icon: '📧', label: 'メール', value: 'info@juneberry.jp' },
  { icon: '📱', label: 'SNS', value: '@juneberry_leotard' },
  { icon: '🕐', label: '営業時間', value: '平日 10:00〜18:00' },
]

function handleSubmit() {
  if (!email.value) return
  submitted.value = true
}
</script>

<template>
  <section id="contact" class="contact section">
    <div class="container">
      <div class="box">
        <p class="eyebrow center">Contact & Newsletter</p>
        <h2 class="section-title center">最新情報をお届け</h2>

        <p class="desc">
          新商品・季節限定カラー・キャンペーン情報をいち早くお届けします。<br>
          メールアドレスを登録して、June BERRY の世界をお楽しみください。
        </p>

        <Transition name="fade" mode="out-in">
          <form v-if="!submitted" class="form" @submit.prevent="handleSubmit" novalidate>
            <div class="form-row">
              <label class="sr-only" for="newsletter-email">メールアドレス</label>
              <input
                id="newsletter-email"
                v-model="email"
                type="email"
                placeholder="your@email.com"
                required
                aria-required="true"
              />
              <button type="submit" class="btn btn-primary">登録する</button>
            </div>
            <p class="note">プライバシーポリシーに同意の上でご登録ください。いつでも解除できます。</p>
          </form>

          <div v-else class="success" role="status">
            ご登録ありがとうございます！素敵な情報をお届けします 🌸
          </div>
        </Transition>

        <div class="info">
          <div v-for="item in contactInfo" :key="item.label" class="info-item">
            <span class="info-icon">{{ item.icon }}</span>
            <div>
              <strong>{{ item.label }}</strong>
              <p>{{ item.value }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact { background: var(--ivory); }

.box {
  background: var(--white);
  border-radius: calc(var(--radius) * 1.5);
  padding: 4rem;
  box-shadow: var(--shadow-md);
  max-width: 780px;
  margin-inline: auto;
}

.desc {
  text-align: center;
  color: var(--text-muted);
  line-height: 2;
  margin-bottom: 2.5rem;
}

.form {
  max-width: 480px;
  margin-inline: auto;
  margin-bottom: 1rem;
}

.form-row {
  display: flex;
  gap: 0.75rem;
  margin-bottom: 0.75rem;
}

.form-row input {
  flex: 1;
  padding: 0.85em 1.2em;
  border: 1.5px solid var(--berry-pale);
  border-radius: 50px;
  font-family: var(--font-sans);
  font-size: 0.9rem;
  color: var(--text);
  background: var(--cream);
  outline: none;
  transition: border-color var(--transition), box-shadow var(--transition);
}

.form-row input:focus {
  border-color: var(--berry-light);
  box-shadow: 0 0 0 3px rgba(166, 61, 114, 0.15);
}

.note {
  text-align: center;
  font-size: 0.75rem;
  color: var(--text-muted);
}

.success {
  text-align: center;
  color: var(--berry);
  font-weight: 500;
  padding: 1.5rem;
  background: var(--berry-pale);
  border-radius: var(--radius);
  max-width: 480px;
  margin-inline: auto;
}

.info {
  display: flex;
  justify-content: center;
  gap: 3rem;
  margin-top: 3rem;
  padding-top: 2.5rem;
  border-top: 1px solid var(--berry-pale);
  flex-wrap: wrap;
}

.info-item {
  display: flex;
  gap: 0.8rem;
  align-items: flex-start;
}

.info-icon { font-size: 1.3rem; }

.info-item strong {
  display: block;
  font-size: 0.75rem;
  letter-spacing: 0.1em;
  color: var(--berry);
  margin-bottom: 0.2rem;
}

.info-item p {
  font-size: 0.875rem;
  color: var(--text-muted);
}

/* Transition */
.fade-enter-active, .fade-leave-active { transition: opacity 0.4s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; }

@media (max-width: 768px) {
  .box { padding: 2.5rem 1.5rem; }
  .form-row { flex-direction: column; }
  .info { gap: 1.5rem; flex-direction: column; align-items: center; }
}

@media (max-width: 480px) {
  .box { padding: 2rem 1rem; }
}
</style>
