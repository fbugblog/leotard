<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)

const programs = [
  {
    num: '01',
    tag: 'JUNIOR',
    title: '新体操クラス',
    subtitle: 'ジュニア・子どもクラス',
    age: '3歳〜中学生',
    desc: '新体操の基礎から競技レベルまで幅広く対応。楽しみながらリズム感・柔軟性・表現力を身につけます。',
    points: ['週1〜週3コース', '初心者〜経験者対応', '発表会年2回', '手具練習（ボール・リボン）'],
    accent: 'pink',
  },
  {
    num: '02',
    tag: 'ADULT',
    title: 'ボディメイキング',
    subtitle: '大人向けフィットネス',
    age: '18歳〜',
    desc: '新体操の動きを取り入れた大人のためのボディメイキング。美しい姿勢と引き締まった体を目指します。',
    points: ['週1〜週2コース', '体力・経験不問', 'ストレッチ・コア強化', '姿勢改善プログラム'],
    accent: 'violet',
  },
  {
    num: '03',
    tag: 'COMPETITIVE',
    title: '選手育成コース',
    subtitle: 'アドバンスド・競技コース',
    age: '経験者対象',
    desc: '大会・発表会を目指す本格コース。個人の技術・演技力を最大限に引き出す集中指導を行います。',
    points: ['週3〜週5', '大会・発表会サポート', '個別プログラム設計', '衣装・音楽アドバイス'],
    accent: 'pink',
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
  <section id="programs" class="programs section" ref="sectionRef">
    <div class="bg-label" aria-hidden="true">PROGRAMS</div>

    <div class="container">
      <div class="section-head scroll-in">
        <div class="head-left">
          <span class="eyebrow">PROGRAMS</span>
          <h2 class="display-title">クラス紹介</h2>
        </div>
        <p class="section-sub scroll-in" style="transition-delay:.08s">
          年齢・経験・目標に合わせて、<br>最適なクラスをお選びいただけます。
        </p>
      </div>

      <div class="cards">
        <article
          v-for="(p, i) in programs"
          :key="p.num"
          class="card scroll-in"
          :class="`card--${p.accent}`"
          :style="{ transitionDelay: `${i * 0.12}s` }"
        >
          <div class="card-num" aria-hidden="true">{{ p.num }}</div>
          <div class="card-top">
            <span class="card-tag">{{ p.tag }}</span>
            <span class="card-age">{{ p.age }}</span>
          </div>
          <h3 class="card-title">{{ p.title }}</h3>
          <p class="card-subtitle">{{ p.subtitle }}</p>
          <p class="card-desc">{{ p.desc }}</p>
          <ul class="card-points">
            <li v-for="pt in p.points" :key="pt">
              <span class="pt-icon" aria-hidden="true">✓</span>
              {{ pt }}
            </li>
          </ul>
        </article>
      </div>

      <div class="programs-footer scroll-in">
        <p>※ クラスの詳細・体験レッスンのご予約はお問い合わせください。</p>
        <button
          class="btn btn-outline"
          @click="document.querySelector('#contact')?.scrollIntoView({ behavior: 'smooth' })"
        >
          お問い合わせはこちら →
        </button>
      </div>
    </div>
  </section>
</template>

<style scoped>
.programs {
  background: var(--surface);
  position: relative;
  overflow: hidden;
}

/* Background label */
.bg-label {
  position: absolute;
  font-family: var(--font-display);
  font-size: clamp(5rem, 16vw, 14rem);
  font-weight: 800;
  color: transparent;
  -webkit-text-stroke: 1px rgba(240, 78, 132, 0.045);
  letter-spacing: -0.04em;
  top: 0; right: -2rem;
  pointer-events: none;
  user-select: none;
  white-space: nowrap;
  line-height: 1;
}

/* Section head */
.section-head {
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: end;
  gap: 3rem;
  margin-bottom: 4rem;
}

.head-left { display: flex; flex-direction: column; gap: 0.5rem; }

.head-left .display-title { color: var(--text); }

.section-sub {
  font-size: 0.95rem;
  color: var(--text-muted);
  line-height: 2;
  padding-bottom: 0.2rem;
}

/* Cards */
.cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  margin-bottom: 3rem;
}

.card {
  position: relative;
  border-radius: var(--radius-lg);
  overflow: hidden;
  background: var(--body-bg);
  border: 1.5px solid var(--border);
  padding: 2rem;
  transition: transform var(--transition), box-shadow var(--transition),
              border-color var(--transition),
              opacity 0.85s var(--ease), transform 0.85s var(--ease);
}

.card:hover {
  transform: translateY(-8px);
  box-shadow: var(--shadow-md);
}

.card--pink:hover { border-color: var(--pink-200); }
.card--violet:hover { border-color: var(--violet-200); }

/* Card number (decorative background) */
.card-num {
  position: absolute;
  top: 1rem; right: 1.2rem;
  font-family: var(--font-display);
  font-size: 4rem;
  font-weight: 800;
  color: transparent;
  -webkit-text-stroke: 1.5px var(--border);
  line-height: 1;
  pointer-events: none;
  user-select: none;
  transition: -webkit-text-stroke-color var(--transition);
}

.card--pink:hover .card-num { -webkit-text-stroke-color: var(--pink-200); }
.card--violet:hover .card-num { -webkit-text-stroke-color: var(--violet-200); }

.card-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.2rem;
}

.card-tag {
  font-family: var(--font-display);
  font-size: 0.58rem;
  font-weight: 700;
  letter-spacing: 0.22em;
}

.card--pink .card-tag { color: var(--pink); }
.card--violet .card-tag { color: var(--violet); }

.card-age {
  font-family: var(--font-display);
  font-size: 0.62rem;
  color: var(--text-muted);
  background: var(--surface);
  border: 1px solid var(--border-mid);
  padding: 0.25em 0.7em;
  border-radius: 50px;
}

.card-title {
  font-family: var(--font-serif);
  font-size: 1.6rem;
  font-weight: 600;
  color: var(--text);
  margin-bottom: 0.25rem;
  line-height: 1.2;
}

.card-subtitle {
  font-family: var(--font-display);
  font-size: 0.68rem;
  letter-spacing: 0.08em;
  color: var(--text-muted);
  margin-bottom: 1.2rem;
}

.card-desc {
  font-size: 0.84rem;
  color: var(--text-mid);
  line-height: 1.9;
  margin-bottom: 1.5rem;
  padding-bottom: 1.5rem;
  border-bottom: 1px solid var(--border);
}

.card-points {
  display: flex;
  flex-direction: column;
  gap: 0.55rem;
}

.card-points li {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  font-size: 0.8rem;
  color: var(--text-muted);
  line-height: 1.5;
}

.pt-icon { flex-shrink: 0; font-weight: 700; }
.card--pink .pt-icon { color: var(--pink); }
.card--violet .pt-icon { color: var(--violet); }

/* Footer row */
.programs-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1.5rem 2rem;
  background: var(--pink-50);
  border-radius: var(--radius);
  border: 1px solid var(--pink-200);
  flex-wrap: wrap;
  gap: 1rem;
}

.programs-footer p {
  font-size: 0.82rem;
  color: var(--text-mid);
}

/* Responsive */
@media (max-width: 1000px) {
  .section-head { grid-template-columns: 1fr; gap: 1.5rem; }
}

@media (max-width: 900px) {
  .cards { grid-template-columns: 1fr; }
}

@media (max-width: 600px) {
  .programs-footer { flex-direction: column; align-items: flex-start; }
}
</style>
