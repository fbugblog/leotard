<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)

const pillars = [
  { num: '01', title: '技術と美しさ', desc: '正しい技術と美しい動きは表裏一体。基礎から丁寧に、本物の動きを学びます。' },
  { num: '02', title: '一人ひとりに寄り添う', desc: '少人数制で、各生徒の個性と目標に合わせたオーダーメイドの指導を大切にしています。' },
  { num: '03', title: '楽しく続けられる', desc: '通うことが楽しくなる雰囲気づくりを最優先に、長く続けられる環境を整えています。' },
]

onMounted(() => {
  const obs = new IntersectionObserver(
    es => es.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); obs.unobserve(e.target) } }),
    { threshold: 0.12 }
  )
  sectionRef.value?.querySelectorAll('.scroll-in').forEach(el => obs.observe(el))
})
</script>

<template>
  <section id="concept" class="concept section" ref="sectionRef">
    <div class="container">

      <!-- Header row with large section number -->
      <div class="header-row scroll-in">
        <div class="header-num" aria-hidden="true">01</div>
        <div class="header-info">
          <span class="eyebrow">CONCEPT</span>
          <h2 class="concept-title">
            <span class="title-reg">体を動かす喜びと、</span>
            <em class="title-em">美しさを追求する。</em>
          </h2>
        </div>
      </div>

      <!-- Main body -->
      <div class="body-grid">
        <div class="body-text scroll-in" style="transition-delay:.08s">
          <p>
            GRACE STUDIOは、新体操とボディメイキングを組み合わせた新しいタイプのスタジオです。
            子どもから大人まで、それぞれのペースで「動く喜び」を体験していただけます。
          </p>
          <p>
            新体操で培われる柔軟性・リズム感・表現力は、日常の体の使い方を根本から変えます。
            ボディメイキングと組み合わせることで、美しい姿勢と引き締まった体をつくることができます。
          </p>
          <p>
            コーチ歴15年・国際大会経験を持つインストラクターが、基礎から丁寧に、楽しく指導します。
          </p>
        </div>

        <!-- Dark decorative block -->
        <div class="deco-block scroll-in" style="transition-delay:.16s" aria-hidden="true">
          <div class="deco-words">
            <span class="deco-w deco-w-dim">MOVE</span>
            <span class="deco-w deco-w-pink">GRACE</span>
            <span class="deco-w deco-w-dim">GROW</span>
          </div>
          <div class="deco-badge">
            <span class="badge-sub">体験レッスン</span>
            <strong class="badge-main">受付中</strong>
          </div>
          <div class="deco-ring" />
        </div>
      </div>

      <!-- 3-pillar grid -->
      <div class="pillars">
        <div
          v-for="(p, i) in pillars"
          :key="p.num"
          class="pillar scroll-in"
          :style="{ transitionDelay: `${0.05 + i * 0.1}s` }"
        >
          <span class="pillar-num" aria-hidden="true">{{ p.num }}</span>
          <h3 class="pillar-title">{{ p.title }}</h3>
          <p class="pillar-desc">{{ p.desc }}</p>
        </div>
      </div>

    </div>
  </section>
</template>

<style scoped>
.concept {
  background: var(--body-bg);
}

/* Header row */
.header-row {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 2.5rem;
  align-items: end;
  margin-bottom: 5rem;
}

.header-num {
  font-family: var(--font-display);
  font-size: clamp(5rem, 12vw, 9rem);
  font-weight: 700;
  color: transparent;
  -webkit-text-stroke: 1.5px var(--border-mid);
  line-height: 1;
  letter-spacing: -0.04em;
  user-select: none;
  padding-bottom: 0.2em;
}

.concept-title {
  display: flex;
  flex-direction: column;
  line-height: 1.2;
}

.title-reg {
  font-family: var(--font-serif);
  font-size: clamp(1.6rem, 3.5vw, 2.6rem);
  font-weight: 300;
  color: var(--text-mid);
}

.title-em {
  font-family: var(--font-serif);
  font-size: clamp(1.9rem, 4vw, 3rem);
  font-weight: 400;
  font-style: italic;
  color: var(--pink);
}

/* Body grid */
.body-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: start;
  margin-bottom: 5rem;
}

.body-text p {
  color: var(--text-mid);
  line-height: 2;
  font-size: 0.94rem;
  margin-bottom: 1.2rem;
}

.body-text p:last-child { margin-bottom: 0; }

/* Deco block */
.deco-block {
  position: relative;
  background: var(--charcoal);
  border-radius: var(--radius-lg);
  overflow: hidden;
  aspect-ratio: 4/3;
  display: flex;
  align-items: center;
  justify-content: center;
}

.deco-words {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.2rem;
  z-index: 1;
}

.deco-w {
  font-family: var(--font-display);
  font-size: clamp(1.8rem, 4vw, 3rem);
  font-weight: 800;
  letter-spacing: 0.06em;
  line-height: 1;
}

.deco-w-dim  { color: rgba(255, 255, 255, 0.1); }
.deco-w-pink { color: var(--pink); }

.deco-badge {
  position: absolute;
  bottom: 1.5rem; right: 1.5rem;
  background: var(--pink);
  color: var(--surface);
  padding: 0.65em 1.2em;
  border-radius: var(--radius-sm);
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 0.1rem;
  z-index: 2;
}

.badge-sub {
  font-family: var(--font-display);
  font-size: 0.58rem;
  letter-spacing: 0.12em;
  opacity: 0.8;
}

.badge-main {
  font-family: var(--font-display);
  font-size: 1.05rem;
  font-weight: 700;
  letter-spacing: 0.04em;
}

.deco-ring {
  position: absolute;
  top: -40px; left: -40px;
  width: 200px; height: 200px;
  border-radius: 50%;
  border: 1.5px solid rgba(240, 78, 132, 0.15);
}

/* Pillars */
.pillars {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5px;
  background: var(--border);
  border-radius: var(--radius-lg);
  overflow: hidden;
  border: 1.5px solid var(--border);
}

.pillar {
  background: var(--surface);
  padding: 2.5rem 2rem;
  transition: background var(--transition),
              opacity 0.85s var(--ease), transform 0.85s var(--ease);
}

.pillar:hover { background: var(--pink-50); }

.pillar-num {
  font-family: var(--font-display);
  font-size: 2.2rem;
  font-weight: 700;
  color: transparent;
  -webkit-text-stroke: 1.5px var(--pink-200);
  display: block;
  margin-bottom: 1rem;
  line-height: 1;
  transition: -webkit-text-stroke-color var(--transition);
}

.pillar:hover .pillar-num { -webkit-text-stroke-color: var(--pink); }

.pillar-title {
  font-family: var(--font-display);
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--text);
  margin-bottom: 0.6rem;
}

.pillar-desc {
  font-size: 0.82rem;
  color: var(--text-muted);
  line-height: 1.85;
}

/* Responsive */
@media (max-width: 900px) {
  .header-row { grid-template-columns: 1fr; gap: 1rem; }
  .header-num { font-size: 4rem; }
  .body-grid { grid-template-columns: 1fr; gap: 2.5rem; }
  .pillars { grid-template-columns: 1fr; }
}
</style>
