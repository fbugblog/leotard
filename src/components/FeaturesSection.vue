<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)

const features = [
  { icon: '🪡', title: '国内縫製・品質保証', desc: '熟練の職人による丁寧な縫製で、長く愛用できる耐久性を実現。全品に品質チェックを実施しています。' },
  { icon: '🎨', title: 'カスタムオーダー対応', desc: '生地・カラー・デザインをご希望に合わせてカスタマイズ。チームや発表会の衣装としても対応可能です。' },
  { icon: '📦', title: '丁寧なパッケージ', desc: 'ギフトにもぴったりな上品なボックスでお届け。大切な方へのプレゼントにも喜ばれています。' },
  { icon: '💬', title: '専門スタッフによるサポート', desc: 'バレエ・体操経験者のスタッフが、サイズ選びや素材のご相談に丁寧にお答えします。' },
  { icon: '🔄', title: '30日間返品・交換保証', desc: 'サイズが合わない場合も安心。購入から30日以内であれば、未使用品に限り無料で交換・返品対応します。' },
  { icon: '✈️', title: '全国送料無料', desc: '国内全域への送料は一切かかりません。まとめ買いや定期購入でさらにお得な特典もご用意しています。' },
]

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); observer.unobserve(e.target) } }),
    { threshold: 0.1 }
  )
  sectionRef.value?.querySelectorAll('.fade-in').forEach(el => observer.observe(el))
})
</script>

<template>
  <section id="features" class="features section" ref="sectionRef">
    <div class="features-bg" aria-hidden="true"></div>
    <div class="container">
      <p class="eyebrow center">Why June BERRY</p>
      <h2 class="section-title center">選ばれる理由</h2>

      <div class="grid">
        <div
          v-for="(f, i) in features"
          :key="f.title"
          class="item fade-in"
          :style="{ transitionDelay: `${i * 0.08}s` }"
        >
          <div class="item__icon">{{ f.icon }}</div>
          <h3>{{ f.title }}</h3>
          <p>{{ f.desc }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.features {
  position: relative;
  background: var(--white);
}

.features-bg {
  position: absolute;
  inset: 0;
  background:
    radial-gradient(circle at 10% 20%, rgba(243, 214, 232, 0.3) 0%, transparent 50%),
    radial-gradient(circle at 90% 80%, rgba(243, 214, 232, 0.2) 0%, transparent 50%);
  pointer-events: none;
}

.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  position: relative;
}

.item {
  text-align: center;
  padding: 2rem 1.5rem;
  border-radius: var(--radius);
  background: var(--ivory);
  transition: transform var(--transition), box-shadow var(--transition), opacity 0.7s ease;
}

.item:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-md);
}

.item__icon {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.item h3 {
  font-family: var(--font-serif);
  font-size: 1.1rem;
  font-weight: 600;
  color: var(--berry);
  margin-bottom: 0.8rem;
}

.item p {
  font-size: 0.875rem;
  color: var(--text-muted);
  line-height: 1.8;
}

@media (max-width: 1024px) {
  .grid { grid-template-columns: repeat(2, 1fr); }
}

@media (max-width: 640px) {
  .grid { grid-template-columns: 1fr; gap: 1.2rem; }
}
</style>
