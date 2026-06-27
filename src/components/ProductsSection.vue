<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)

const products = [
  {
    id: 'competition',
    num: '01',
    tag: 'Competition',
    title: '競技用レオタード',
    icon: '✨',
    desc: '大会・発表会の舞台で輝くための一枚。ラインストーン・スパンコール・スウロフスキークリスタルを組み合わせた華やかな装飾と、激しい演技に耐える高強度素材を両立。照明を最大限に引き出すデザインで、採点競技での印象を高めます。',
    specs: ['素材：マイクロファイバー + ラメ / スパンデックス混', 'サイズ：100cm〜LL / カスタムサイズ対応', '装飾：スワロフスキー・スパンコール・ラインストーン', 'カラー：オーダーカラー対応'],
    accent: '#7A1B4A',
    accentLight: '#F8D6E8',
    featured: true,
  },
  {
    id: 'practice',
    num: '02',
    tag: 'Practice',
    title: '練習用レオタード',
    icon: '🎀',
    desc: '毎日のレッスンに寄り添う実用的な一枚。優れた伸縮性と耐久性で長時間の練習でも快適。豊富なカラーバリエーションで曜日や気分によって着替える楽しさも。洗濯耐性も考慮した素材を使用しています。',
    specs: ['素材：ナイロン85% / ポリウレタン15%', 'サイズ：90cm〜XL', 'カラー：50色以上のベーシックカラー', '特長：速乾・型崩れしにくい設計'],
    accent: '#C2547A',
    accentLight: '#F5D6E4',
    featured: false,
  },
  {
    id: 'custom',
    num: '03',
    tag: 'Custom Order',
    title: 'オーダーメイド',
    icon: '👑',
    desc: 'チームウェアや個人の発表会衣装を一から制作。生地・カラー・装飾・シルエットまでご要望に合わせてデザイン。プロの衣装師がヒアリングから仕上げまで丁寧に対応します。団体・クラブのまとめ発注にも対応。',
    specs: ['リードタイム：約4〜6週間', 'ロット：1枚から対応', '対応内容：デザイン・生地・装飾すべて選択可', '相談：無料オンライン相談あり'],
    accent: '#BF4E78',
    accentLight: '#F7DCEA',
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
  <section id="products" class="products section" ref="sectionRef">
    <div class="container">
      <div class="section-header fade-in">
        <span class="eyebrow">Collections</span>
        <h2 class="display-title">新体操のための<br>3つのライン</h2>
      </div>

      <div class="list">
        <article
          v-for="(p, i) in products"
          :key="p.id"
          class="item fade-in"
          :class="{ featured: p.featured }"
          :style="{ transitionDelay: `${i * 0.12}s` }"
        >
          <div class="item__num">{{ p.num }}</div>

          <div class="item__icon-wrap" :style="{ background: p.accentLight }">
            <span class="item__icon">{{ p.icon }}</span>
          </div>

          <div class="item__body">
            <span class="item__tag" :style="{ color: p.accent }">{{ p.tag }}</span>
            <h3 class="item__title">{{ p.title }}</h3>
            <p class="item__desc">{{ p.desc }}</p>

            <ul class="item__specs">
              <li v-for="s in p.specs" :key="s">
                <span class="spec-dot" :style="{ background: p.accent }" />
                {{ s }}
              </li>
            </ul>
          </div>

          <div class="item__featured-badge" v-if="p.featured">人気 No.1</div>
          <div class="item__border" :style="{ background: `linear-gradient(to bottom, ${p.accent}, transparent)` }" />
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.products { background: var(--white); }

.section-header {
  margin-bottom: 4rem;
}

.section-header .display-title {
  margin-top: 0.5rem;
  color: var(--dark);
}

.list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.item {
  display: grid;
  grid-template-columns: 64px 120px 1fr;
  gap: 0 2.5rem;
  align-items: start;
  padding: 2.5rem;
  background: var(--cream);
  border-radius: var(--radius);
  position: relative;
  overflow: hidden;
  transition: transform var(--transition), box-shadow var(--transition), opacity 0.75s var(--ease);
}

.item:hover {
  transform: translateX(6px);
  box-shadow: var(--shadow-md);
}

.item.featured {
  background: var(--dark-2);
}

.item.featured .item__title { color: var(--champagne); }
.item.featured .item__desc  { color: rgba(255,255,255,0.6); }
.item.featured .item__specs li { color: rgba(255,255,255,0.55); }

/* Number */
.item__num {
  font-family: var(--font-serif);
  font-size: 3rem;
  font-weight: 300;
  color: rgba(7,4,14,0.12);
  line-height: 1;
  padding-top: 0.25rem;
}

.item.featured .item__num { color: rgba(255,255,255,0.08); }

/* Icon wrap */
.item__icon-wrap {
  width: 80px;
  height: 80px;
  border-radius: var(--radius-sm);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.item__icon { font-size: 2.2rem; }

/* Body */
.item__tag {
  font-size: 0.68rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  font-weight: 500;
  display: block;
  margin-bottom: 0.4rem;
}

.item__title {
  font-family: var(--font-serif);
  font-size: 1.6rem;
  font-weight: 600;
  color: var(--dark);
  margin-bottom: 0.9rem;
}

.item__desc {
  font-size: 0.875rem;
  color: var(--text-muted-dark);
  line-height: 1.9;
  margin-bottom: 1.2rem;
}

.item__specs {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem 1.5rem;
}

.item__specs li {
  font-size: 0.78rem;
  color: var(--text-muted-dark);
  display: flex;
  align-items: center;
  gap: 0.4rem;
}

.spec-dot {
  display: inline-block;
  width: 5px; height: 5px;
  border-radius: 50%;
  flex-shrink: 0;
}

/* Featured badge */
.item__featured-badge {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  background: var(--gold);
  color: var(--dark);
  font-size: 0.68rem;
  font-weight: 500;
  padding: 0.3em 0.9em;
  border-radius: 50px;
  letter-spacing: 0.05em;
}

/* Left accent border */
.item__border {
  position: absolute;
  left: 0; top: 0;
  width: 3px;
  height: 100%;
}

@media (max-width: 768px) {
  .item {
    grid-template-columns: 1fr;
    gap: 1.2rem;
    padding: 2rem 1.5rem;
  }

  .item__num { font-size: 2rem; }
  .item__icon-wrap { width: 64px; height: 64px; }
  .item__icon { font-size: 1.8rem; }
}
</style>
