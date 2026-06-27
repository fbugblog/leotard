<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)

const features = [
  { num: '01', title: '新体操専門の設計', desc: '種目特有の動き（リボン・ボール・フープ・クラブ・ロープ）を熟知した設計。どのポーズでも美しいシルエットを保ちます。' },
  { num: '02', title: '国内職人による縫製', desc: '熟練の職人が一点一点丁寧に仕上げ。高い縫製精度で、激しい演技にも型崩れしません。' },
  { num: '03', title: 'カスタムオーダー対応', desc: '生地・カラー・装飾・シルエットすべてをカスタマイズ可能。チームウェアの一括注文も承ります。' },
  { num: '04', title: '豊富なサイズ展開', desc: 'ジュニア（90cm〜）から大人（3L）まで対応。カスタムサイズにも対応しているので、どんな体型の方にもフィットします。' },
  { num: '05', title: '30日間保証', desc: 'サイズが合わない場合も安心。未使用品に限り購入から30日以内であれば無料で交換・返品対応します。' },
  { num: '06', title: '全国送料無料', desc: '国内全域への送料は完全無料。大切な衣装を傷つけないよう、専用ボックスで丁寧にお届けします。' },
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
  <section id="features" class="features section" ref="sectionRef">
    <div class="container">
      <div class="top fade-in">
        <span class="eyebrow" style="color: rgba(255,255,255,0.4)">Why June BERRY</span>
        <h2 class="display-title" style="color: var(--champagne)">選ばれる理由</h2>
      </div>

      <div class="grid">
        <div
          v-for="(f, i) in features"
          :key="f.num"
          class="item fade-in"
          :style="{ transitionDelay: `${i * 0.08}s` }"
        >
          <div class="item-top">
            <span class="num">{{ f.num }}</span>
            <div class="line" />
          </div>
          <h3>{{ f.title }}</h3>
          <p>{{ f.desc }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.features {
  background: var(--dark);
  position: relative;
  overflow: hidden;
}

.features::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 1px;
  background: linear-gradient(to right, transparent, var(--gold), transparent);
}

.top { margin-bottom: 4rem; }

.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 0;
  border: 1px solid rgba(255,255,255,0.06);
}

.item {
  padding: 2.5rem;
  border-right: 1px solid rgba(255,255,255,0.06);
  border-bottom: 1px solid rgba(255,255,255,0.06);
  transition: background var(--transition), opacity 0.75s var(--ease), transform 0.75s var(--ease);
}

.item:hover { background: rgba(255,255,255,0.03); }

.item:nth-child(3n) { border-right: none; }
.item:nth-child(4), .item:nth-child(5), .item:nth-child(6) { border-bottom: none; }

.item-top {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.2rem;
}

.num {
  font-family: var(--font-serif);
  font-size: 1.4rem;
  font-weight: 300;
  color: var(--gold);
  line-height: 1;
}

.line {
  flex: 1;
  height: 1px;
  background: rgba(255,255,255,0.1);
}

.item h3 {
  font-family: var(--font-serif);
  font-size: 1.1rem;
  font-weight: 600;
  color: var(--champagne);
  margin-bottom: 0.7rem;
}

.item p {
  font-size: 0.85rem;
  color: rgba(255,255,255,0.45);
  line-height: 1.9;
}

@media (max-width: 900px) {
  .grid { grid-template-columns: repeat(2, 1fr); }
  .item:nth-child(3n) { border-right: 1px solid rgba(255,255,255,0.06); }
  .item:nth-child(2n) { border-right: none; }
  .item:nth-child(5), .item:nth-child(6) { border-bottom: none; }
  .item:nth-child(4) { border-bottom: 1px solid rgba(255,255,255,0.06); }
}

@media (max-width: 600px) {
  .grid { grid-template-columns: 1fr; }
  .item { border-right: none; }
  .item:last-child { border-bottom: none; }
}
</style>
