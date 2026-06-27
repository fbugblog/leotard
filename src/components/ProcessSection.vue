<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)

const steps = [
  { num: '01', title: 'お問い合わせ', desc: 'InstagramのDMまたはお問い合わせフォームからご連絡ください。どんな小さなご相談でも歓迎です。' },
  { num: '02', title: 'ヒアリング', desc: 'イメージ・用途・体型・予算・納期などを丁寧にお聞きします。参考画像があればお送りください。' },
  { num: '03', title: 'デザイン提案', desc: 'ヒアリング内容をもとにデザイン案をご提案。修正・調整を重ねて理想の一枚を決定します。' },
  { num: '04', title: 'お見積り確認', desc: '素材・装飾・工数をもとに正式なお見積りをご提示。ご納得いただけたら制作開始です。' },
  { num: '05', title: '制作', desc: '型紙作成・裁断・縫製・装飾貼り付けまで、すべての工程を私一人で丁寧に仕上げます。' },
  { num: '06', title: '完成・お届け', desc: '完成後に写真でご確認いただき、専用ボックスで丁寧に梱包してお届けします。全国送料無料。' },
]

onMounted(() => {
  const obs = new IntersectionObserver(
    (es) => es.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); obs.unobserve(e.target) } }),
    { threshold: 0.08 }
  )
  sectionRef.value?.querySelectorAll('.fade-in').forEach(el => obs.observe(el))
})
</script>

<template>
  <section id="process" class="process section" ref="sectionRef">
    <div class="container">
      <div class="header fade-in">
        <span class="eyebrow">How to Order</span>
        <h2 class="display-title">制作の流れ</h2>
        <p class="header-sub">お問い合わせから完成まで、安心してお任せください。</p>
      </div>

      <div class="steps">
        <div
          v-for="(step, i) in steps"
          :key="step.num"
          class="step fade-in"
          :style="{ transitionDelay: `${i * 0.1}s` }"
        >
          <div class="step__left">
            <div class="step__num">{{ step.num }}</div>
            <div class="step__line" v-if="i < steps.length - 1" />
          </div>
          <div class="step__body">
            <h3 class="step__title">{{ step.title }}</h3>
            <p class="step__desc">{{ step.desc }}</p>
          </div>
        </div>
      </div>

      <div class="cta-block fade-in">
        <p>まずはお気軽にご相談ください。相談・お見積りは無料です。</p>
        <button class="btn btn-gold" onclick="document.querySelector('#contact')?.scrollIntoView({behavior:'smooth'})">
          無料相談・お見積りはこちら
        </button>
      </div>
    </div>
  </section>
</template>

<style scoped>
.process {
  background: var(--cream);
  position: relative;
}

.header { margin-bottom: 3.5rem; }

.header .display-title { color: var(--dark); margin-top: 0.5rem; }

.header-sub {
  margin-top: 0.6rem;
  font-size: 0.9rem;
  color: var(--text-muted-dark);
}

.steps {
  display: flex;
  flex-direction: column;
  gap: 0;
  max-width: 680px;
  margin-bottom: 3.5rem;
}

.step {
  display: grid;
  grid-template-columns: 80px 1fr;
  gap: 0 2rem;
  transition: opacity 0.75s var(--ease);
}

.step__left {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0;
}

.step__num {
  width: 52px; height: 52px;
  border-radius: 50%;
  background: var(--gold);
  color: var(--white);
  font-family: var(--font-serif);
  font-size: 1rem;
  font-weight: 600;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  z-index: 1;
}

.step__line {
  width: 1.5px;
  flex: 1;
  min-height: 2rem;
  background: linear-gradient(to bottom, var(--gold), rgba(191,78,120,0.2));
  margin: 0.25rem 0;
}

.step__body {
  padding-bottom: 2.5rem;
}

.step:last-child .step__body { padding-bottom: 0; }

.step__title {
  font-family: var(--font-serif);
  font-size: 1.1rem;
  font-weight: 600;
  color: var(--dark);
  margin-bottom: 0.4rem;
  padding-top: 0.75rem;
}

.step__desc {
  font-size: 0.875rem;
  color: var(--text-muted-dark);
  line-height: 1.85;
}

.cta-block {
  display: flex;
  align-items: center;
  gap: 2rem;
  padding: 2rem 2.5rem;
  background: var(--white);
  border-radius: var(--radius);
  border: 1px solid rgba(191,78,120,0.15);
  flex-wrap: wrap;
}

.cta-block p {
  font-size: 0.9rem;
  color: var(--text-muted-dark);
  flex: 1;
  min-width: 200px;
  line-height: 1.6;
}

@media (max-width: 600px) {
  .step { grid-template-columns: 56px 1fr; gap: 0 1.2rem; }
  .step__num { width: 42px; height: 42px; font-size: 0.85rem; }
  .cta-block { flex-direction: column; align-items: flex-start; }
}
</style>
