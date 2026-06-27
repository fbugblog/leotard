<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)

const stats = [
  { num: '100+', label: 'カラーバリエーション' },
  { num: '30日', label: '返品・交換保証' },
  { num: '全国', label: '送料無料' },
]

onMounted(() => {
  const obs = new IntersectionObserver(
    (es) => es.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); obs.unobserve(e.target) } }),
    { threshold: 0.1 }
  )
  sectionRef.value?.querySelectorAll('.fade-in').forEach(el => obs.observe(el))
})
</script>

<template>
  <section id="concept" class="concept section" ref="sectionRef">
    <div class="container">
      <div class="header-row fade-in">
        <span class="eyebrow">Our Concept</span>
        <div class="divider" aria-hidden="true" />
      </div>

      <div class="grid">
        <div class="headline-col fade-in" style="transition-delay:.1s">
          <h2 class="display-title">
            演技に宿る<br>
            <em>美しさ</em>のために
          </h2>
          <p class="accent-text">新体操専門店として、競技者の「美」に向き合い続けます。</p>
        </div>

        <div class="text-col fade-in" style="transition-delay:.2s">
          <p>
            June BERRY は新体操に特化したレオタード専門店です。
            採点競技において衣装は演技の一部――審判の目に映る美しさ、観客を惹きつける輝き、
            そして選手自身が感じる自信のすべてが、レオタード一枚に宿っています。
          </p>
          <p>
            私たちはバレエや体操とは異なる新体操ならではの動き――
            リボン、ボール、フープ、クラブ、ロープ――を熟知したうえで、
            どんな演技でも美しいシルエットを保てる設計をしています。
          </p>
          <p>
            "June" は輝きと美しさが絶頂を迎える季節を、
            "BERRY" は小さくても濃密な美しさを表しています。
            どちらもあなたの演技に添えたい言葉です。
          </p>

          <div class="stats">
            <div class="stat" v-for="s in stats" :key="s.num">
              <span class="stat-num">{{ s.num }}</span>
              <span class="stat-label">{{ s.label }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="bg-accent" aria-hidden="true" />
  </section>
</template>

<style scoped>
.concept {
  background: var(--cream);
  position: relative;
  overflow: hidden;
}

.header-row {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  margin-bottom: 4rem;
}

.divider {
  flex: 1;
  height: 1px;
  background: linear-gradient(to right, var(--gold), transparent);
}

.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 6rem;
  align-items: start;
}

.display-title {
  font-size: clamp(2.4rem, 5.5vw, 4rem);
  font-weight: 300;
  color: var(--dark);
  line-height: 1.15;
  margin-bottom: 1.5rem;
}

.display-title em {
  font-style: italic;
  color: var(--purple);
}

.accent-text {
  font-family: var(--font-serif);
  font-size: 1.05rem;
  font-style: italic;
  color: var(--gold);
}

.text-col p {
  color: var(--text-muted-dark);
  margin-bottom: 1.1rem;
  line-height: 1.9;
}

.stats {
  display: flex;
  gap: 2.5rem;
  margin-top: 2.5rem;
  padding-top: 2rem;
  border-top: 1px solid rgba(7,4,14,0.08);
}

.stat { display: flex; flex-direction: column; gap: 0.2rem; }

.stat-num {
  font-family: var(--font-serif);
  font-size: 2rem;
  font-weight: 600;
  color: var(--purple);
  line-height: 1;
}

.stat-label {
  font-size: 0.72rem;
  letter-spacing: 0.1em;
  color: var(--text-muted-dark);
}

.bg-accent {
  position: absolute;
  top: -80px; right: -120px;
  width: 500px; height: 500px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(74, 27, 122, 0.06), transparent 70%);
  pointer-events: none;
}

@media (max-width: 900px) {
  .grid { grid-template-columns: 1fr; gap: 3rem; }
}

@media (max-width: 480px) {
  .stats { gap: 1.5rem; }
}
</style>
