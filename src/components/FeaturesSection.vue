<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)

const features = [
  {
    num: '01',
    icon: '👥',
    title: '少人数制',
    desc: '1クラス最大8名の少人数制。一人ひとりの動きを丁寧に確認し、個別フィードバックを行います。',
    dark: true,
  },
  {
    num: '02',
    icon: '🏆',
    title: 'プロ指導',
    desc: '国際大会出場経験のあるコーチが直接指導。本物の技術と美しさを丁寧にお伝えします。',
    dark: false,
  },
  {
    num: '03',
    icon: '🌸',
    title: '全年齢対応',
    desc: '3歳の子どもから大人まで対応。ご家族で一緒に通っていただけます。',
    dark: false,
  },
  {
    num: '04',
    icon: '✨',
    title: '本格設備',
    desc: '専用フロア・全面鏡張りスタジオ・プロ仕様の手具など、本格的な練習環境を完備しています。',
    dark: true,
  },
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
  <section id="features" class="features section" ref="sectionRef">
    <div class="container">

      <div class="section-head scroll-in">
        <div class="head-inner">
          <span class="eyebrow">FEATURES</span>
          <h2 class="display-title">GRACEが選ばれる理由</h2>
        </div>
        <div class="head-num" aria-hidden="true">04</div>
      </div>

      <div class="bento">
        <div
          v-for="(f, i) in features"
          :key="f.num"
          class="cell scroll-in"
          :class="{ 'cell--dark': f.dark }"
          :style="{ transitionDelay: `${i * 0.1}s` }"
        >
          <div class="cell-bg-num" aria-hidden="true">{{ f.num }}</div>
          <div class="cell-icon">{{ f.icon }}</div>
          <h3 class="cell-title">{{ f.title }}</h3>
          <p class="cell-desc">{{ f.desc }}</p>
        </div>
      </div>

    </div>
  </section>
</template>

<style scoped>
.features { background: var(--body-bg); }

/* Section head */
.section-head {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: 3.5rem;
  gap: 2rem;
}

.head-inner {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.head-inner .display-title { color: var(--text); }

.head-num {
  font-family: var(--font-display);
  font-size: clamp(4rem, 10vw, 8rem);
  font-weight: 800;
  color: transparent;
  -webkit-text-stroke: 1.5px var(--border-mid);
  line-height: 1;
  letter-spacing: -0.04em;
  user-select: none;
  flex-shrink: 0;
}

/* Bento grid */
.bento {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.5rem;
}

.cell {
  position: relative;
  border-radius: var(--radius-lg);
  padding: 2.5rem 2rem;
  overflow: hidden;
  background: var(--surface);
  border: 1.5px solid var(--border);
  transition: transform var(--transition), box-shadow var(--transition),
              opacity 0.85s var(--ease), transform 0.85s var(--ease);
}

.cell:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-md);
}

.cell--dark {
  background: var(--charcoal);
  border-color: transparent;
}

.cell--dark:hover {
  box-shadow: 0 12px 40px rgba(22, 12, 20, 0.3);
}

/* Background number */
.cell-bg-num {
  position: absolute;
  bottom: -0.8rem; right: 0.8rem;
  font-family: var(--font-display);
  font-size: 5.5rem;
  font-weight: 800;
  color: transparent;
  -webkit-text-stroke: 1.5px;
  line-height: 1;
  pointer-events: none;
  user-select: none;
}

.cell:not(.cell--dark) .cell-bg-num { -webkit-text-stroke-color: var(--border); }
.cell--dark .cell-bg-num { -webkit-text-stroke-color: rgba(255, 255, 255, 0.08); }

/* Cell content */
.cell-icon {
  font-size: 2rem;
  line-height: 1;
  margin-bottom: 1.2rem;
}

.cell-title {
  font-family: var(--font-display);
  font-size: 1.05rem;
  font-weight: 700;
  margin-bottom: 0.75rem;
}

.cell:not(.cell--dark) .cell-title { color: var(--text); }
.cell--dark .cell-title { color: var(--surface); }

.cell-desc {
  font-size: 0.82rem;
  line-height: 1.85;
}

.cell:not(.cell--dark) .cell-desc { color: var(--text-muted); }
.cell--dark .cell-desc { color: rgba(255, 255, 255, 0.45); }

/* Responsive */
@media (max-width: 1000px) {
  .bento { grid-template-columns: repeat(2, 1fr); }
}

@media (max-width: 600px) {
  .bento { grid-template-columns: 1fr; }
  .section-head { flex-direction: column; align-items: flex-start; }
  .head-num { font-size: 3.5rem; }
}
</style>
