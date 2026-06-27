<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)

const plans = [
  {
    tag: 'Full Order',
    title: 'フルオーダー',
    price: '¥35,000',
    unit: '〜',
    desc: 'デザイン・生地・装飾すべてを一から制作。大会・発表会・チームウェアに最適。',
    includes: [
      'デザインヒアリング（無料）',
      '生地・カラー選定',
      'ストーン・スパンコール装飾',
      'カスタムサイズ対応',
      'お見積り後確定',
    ],
    accent: '#7A1B4A',
    featured: true,
  },
  {
    tag: 'Remake',
    title: 'リメイク',
    price: '¥15,000',
    unit: '〜',
    desc: '今あるレオタードの補修・装飾追加・カラー変更など。思い出の一枚をよみがえらせます。',
    includes: [
      '状態確認・お見積り',
      '補修・修繕',
      '装飾追加・変更',
      'サイズ調整',
      '内容により変動あり',
    ],
    accent: '#BF4E78',
    featured: false,
  },
  {
    tag: 'Decoration',
    title: '装飾追加のみ',
    price: '¥8,000',
    unit: '〜',
    desc: 'お手持ちのレオタードへストーン・スパンコールを追加。手軽に華やかさをプラス。',
    includes: [
      'デザイン相談',
      'ストーン・スパンコール貼り付け',
      '着用イメージ確認',
      '追加範囲により変動',
    ],
    accent: '#C2547A',
    featured: false,
  },
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
  <section id="pricing" class="pricing section" ref="sectionRef">
    <div class="container">
      <div class="header fade-in">
        <span class="eyebrow" style="color:rgba(255,255,255,0.4)">Pricing</span>
        <h2 class="display-title" style="color:var(--champagne)">料金の目安</h2>
        <p class="header-note">
          実際の金額はヒアリング後にお見積りします。まずはお気軽にご相談ください。
        </p>
      </div>

      <div class="plans">
        <div
          v-for="(plan, i) in plans"
          :key="plan.tag"
          class="plan fade-in"
          :class="{ featured: plan.featured }"
          :style="{ transitionDelay: `${i * 0.12}s` }"
        >
          <div class="plan__top">
            <span class="plan__tag" :style="{ color: plan.accent }">{{ plan.tag }}</span>
            <h3 class="plan__title">{{ plan.title }}</h3>
            <div class="plan__price">
              <span class="plan__amount">{{ plan.price }}</span>
              <span class="plan__unit">{{ plan.unit }}</span>
            </div>
            <p class="plan__desc">{{ plan.desc }}</p>
          </div>
          <ul class="plan__includes">
            <li v-for="item in plan.includes" :key="item">
              <span class="check" :style="{ color: plan.accent }">✓</span>
              {{ item }}
            </li>
          </ul>
          <div class="plan__badge" v-if="plan.featured">人気</div>
        </div>
      </div>

      <p class="note fade-in">
        ※ 価格はすべて税込・送料無料。チームウェアなど枚数が多い場合は別途ご相談ください。
      </p>
    </div>
  </section>
</template>

<style scoped>
.pricing {
  background: var(--dark);
  position: relative;
}

.pricing::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 1px;
  background: linear-gradient(to right, transparent, rgba(191,78,120,0.4), transparent);
}

.header { margin-bottom: 3.5rem; }

.header-note {
  margin-top: 0.8rem;
  font-size: 0.875rem;
  color: rgba(255,255,255,0.4);
  line-height: 1.8;
}

.plans {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.plan {
  background: var(--dark-2);
  border-radius: var(--radius);
  padding: 2rem;
  position: relative;
  border: 1px solid rgba(255,255,255,0.06);
  transition: transform var(--transition), box-shadow var(--transition), opacity 0.75s var(--ease);
}

.plan:hover {
  transform: translateY(-4px);
  box-shadow: 0 16px 48px rgba(0,0,0,0.3);
}

.plan.featured { border-color: rgba(191,78,120,0.4); background: var(--dark-3); }

.plan__tag {
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  font-weight: 500;
  display: block;
  margin-bottom: 0.4rem;
}

.plan__title {
  font-family: var(--font-serif);
  font-size: 1.4rem;
  font-weight: 600;
  color: var(--champagne);
  margin-bottom: 1rem;
}

.plan__price {
  display: flex;
  align-items: baseline;
  gap: 0.2em;
  margin-bottom: 0.8rem;
}

.plan__amount {
  font-family: var(--font-serif);
  font-size: 2.2rem;
  font-weight: 600;
  color: var(--white);
}

.plan__unit { font-size: 1rem; color: rgba(255,255,255,0.5); }

.plan__desc {
  font-size: 0.82rem;
  color: rgba(255,255,255,0.45);
  line-height: 1.8;
  margin-bottom: 1.5rem;
  padding-bottom: 1.5rem;
  border-bottom: 1px solid rgba(255,255,255,0.06);
}

.plan__includes { display: flex; flex-direction: column; gap: 0.55rem; }

.plan__includes li {
  font-size: 0.8rem;
  color: rgba(255,255,255,0.55);
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.check { font-weight: 700; flex-shrink: 0; }

.plan__badge {
  position: absolute;
  top: 1rem; right: 1rem;
  background: var(--gold);
  color: var(--dark);
  font-size: 0.65rem;
  font-weight: 600;
  padding: 0.25em 0.7em;
  border-radius: 50px;
}

.note {
  font-size: 0.78rem;
  color: rgba(255,255,255,0.3);
  text-align: center;
}

@media (max-width: 900px) {
  .plans { grid-template-columns: 1fr; }
}
</style>
