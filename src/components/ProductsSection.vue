<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)

const products = [
  {
    id: 'ballet',
    tag: 'Ballet Line',
    title: 'バレエライン',
    icon: '🩰',
    bgClass: 'bg-ballet',
    featured: false,
    desc: 'クラシックな優雅さと現代的なデザインが融合。舞台映えするカッティングと、長時間のレッスンでも快適な伸縮素材を採用。ジュニアサイズから大人サイズまで対応。',
    specs: ['素材：ナイロン85% / ポリウレタン15%', 'サイズ：90cm〜XL', 'カラー：20色以上'],
  },
  {
    id: 'gym',
    tag: 'Gymnastics Line',
    title: '体操ライン',
    icon: '🤸',
    bgClass: 'bg-gym',
    featured: true,
    desc: '競技・演技の激しい動きに耐える高強度素材を使用。ラインストーンやスパンコールによる華やかな装飾で、採点競技での存在感を高めます。',
    specs: ['素材：マイクロファイバー + ラメ素材', 'サイズ：100cm〜LL', 'カラー：オーダーカラー対応'],
  },
  {
    id: 'fitness',
    tag: 'Fitness Line',
    title: 'フィットネスライン',
    icon: '💪',
    bgClass: 'bg-fitness',
    featured: false,
    desc: 'ヨガ・エアロビクス・ダンスフィットネスに最適。吸湿速乾素材で快適さをキープ。カジュアルに着こなせるスポーティなデザインから上品なスタイルまで揃えています。',
    specs: ['素材：ポリエステル / スパンデックス混', 'サイズ：S〜3L（大きいサイズ対応）', 'カラー：季節限定カラーあり'],
  },
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
  <section id="products" class="products section" ref="sectionRef">
    <div class="container">
      <p class="eyebrow center">Collections</p>
      <h2 class="section-title center">コレクション</h2>
      <p class="desc center">シーンと目的に合わせた3つのラインナップをご用意しています。</p>

      <div class="grid">
        <article
          v-for="(p, i) in products"
          :key="p.id"
          class="card fade-in"
          :class="{ 'card--featured': p.featured }"
          :style="{ transitionDelay: `${i * 0.12}s` }"
        >
          <div class="card__badge" v-if="p.featured">人気 No.1</div>

          <div class="card__visual" :class="p.bgClass">
            <span class="card__icon">{{ p.icon }}</span>
          </div>

          <div class="card__body">
            <span class="card__tag">{{ p.tag }}</span>
            <h3 class="card__title">{{ p.title }}</h3>
            <p class="card__desc">{{ p.desc }}</p>
            <ul class="card__specs">
              <li v-for="s in p.specs" :key="s">{{ s }}</li>
            </ul>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.products { background: var(--ivory); }

.desc {
  color: var(--text-muted);
  max-width: 42ch;
  margin-inline: auto;
  margin-bottom: 3rem;
}

.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.card {
  background: var(--white);
  border-radius: var(--radius);
  overflow: hidden;
  box-shadow: var(--shadow-sm);
  transition: transform var(--transition), box-shadow var(--transition), opacity 0.7s ease;
  position: relative;
  display: flex;
  flex-direction: column;
}

.card:hover {
  transform: translateY(-8px);
  box-shadow: var(--shadow-lg);
}

.card--featured { border: 2px solid var(--berry-light); }

.card__badge {
  position: absolute;
  top: 1rem; right: 1rem;
  background: var(--berry);
  color: var(--white);
  font-size: 0.7rem;
  padding: 0.3em 0.9em;
  border-radius: 50px;
  letter-spacing: 0.05em;
  z-index: 1;
}

.card__visual {
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  position: relative;
}

.bg-ballet  { background: linear-gradient(135deg, #F3D6E8 0%, #FAD2E8 100%); }
.bg-gym     { background: linear-gradient(135deg, #E8D6F3 0%, #D2C4E8 100%); }
.bg-fitness { background: linear-gradient(135deg, #D6E8F3 0%, #C4D8E8 100%); }

.card__icon {
  font-size: 4.5rem;
  filter: drop-shadow(0 4px 8px rgba(0,0,0,0.08));
  transition: transform var(--transition);
  line-height: 1;
}

.card:hover .card__icon { transform: scale(1.15) rotate(-5deg); }

.card__body {
  padding: 1.5rem;
  flex: 1;
  display: flex;
  flex-direction: column;
}

.card__tag {
  font-size: 0.7rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--berry-light);
  margin-bottom: 0.4rem;
  display: block;
}

.card__title {
  font-family: var(--font-serif);
  font-size: 1.4rem;
  font-weight: 600;
  color: var(--berry);
  margin-bottom: 0.8rem;
}

.card__desc {
  font-size: 0.875rem;
  color: var(--text-muted);
  line-height: 1.8;
  margin-bottom: 1rem;
  flex: 1;
}

.card__specs {
  border-top: 1px solid var(--berry-pale);
  padding-top: 1rem;
  display: flex;
  flex-direction: column;
  gap: 0.35rem;
}

.card__specs li {
  font-size: 0.8rem;
  color: var(--text-muted);
  padding-left: 1em;
  position: relative;
}

.card__specs li::before {
  content: '·';
  position: absolute;
  left: 0;
  color: var(--berry-light);
}

@media (max-width: 1024px) {
  .grid { grid-template-columns: 1fr 1fr; }
  .grid .card:last-child {
    grid-column: span 2;
    max-width: 480px;
    width: 100%;
    margin-inline: auto;
  }
}

@media (max-width: 640px) {
  .grid { grid-template-columns: 1fr; }
  .grid .card:last-child { grid-column: auto; max-width: none; }
}
</style>
