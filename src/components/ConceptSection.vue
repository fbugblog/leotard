<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)

const credentials = [
  { num: '150枚+', label: '制作実績' },
  { num: '12年', label: 'ハンドメイド歴' },
  { num: '5年', label: 'レオタード専門' },
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
  <section id="story" class="story section" ref="sectionRef">
    <div class="container">
      <div class="header-row fade-in">
        <span class="eyebrow">制作への想い</span>
        <div class="divider" aria-hidden="true" />
      </div>

      <div class="grid">
        <div class="headline-col fade-in" style="transition-delay:.1s">
          <h2 class="display-title">
            手仕事で生まれる、<br>
            <em>あなただけの一枚</em>
          </h2>
          <p class="accent-text">「この一枚を着て輝きたい」と思ってもらえる作品を目指して。</p>

          <div class="stats">
            <div class="stat" v-for="s in credentials" :key="s.num">
              <span class="stat-num">{{ s.num }}</span>
              <span class="stat-label">{{ s.label }}</span>
            </div>
          </div>
        </div>

        <div class="text-col fade-in" style="transition-delay:.2s">
          <p>
            新体操は、音楽・表現・技術が一体となる特別なスポーツ。
            その舞台で選手を彩るレオタードは、自信と美しさを引き立てる大切な存在です。
            「この一枚を着て演技したい」そう感じてもらえる作品を、ひとつひとつ心を込めて制作しています。
          </p>
          <p>
            保育士として10年間、一人ひとり違う子どもたちと向き合ってきた経験が、
            今の制作に生きています。体型・演技スタイル・チームカラー・選手の個性——
            丁寧にヒアリングして、その人だけの一枚を仕上げることがこだわりです。
          </p>
          <p>
            デザインから型紙・縫製・ストーン貼りまで、すべての工程を私一人で担当しています。
            量産品にはできない、手仕事ならではの細やかさと温かさを大切にしています。
          </p>

          <div class="badges">
            <span class="badge">保育士資格保有</span>
            <span class="badge">丁寧なヒアリング</span>
            <span class="badge">全工程ひとりで制作</span>
            <span class="badge">大会着用実績あり</span>
          </div>
        </div>
      </div>
    </div>

    <div class="bg-accent" aria-hidden="true" />
  </section>
</template>

<style scoped>
.story {
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
  font-size: clamp(2rem, 5vw, 3.4rem);
  font-weight: 300;
  color: var(--dark);
  line-height: 1.2;
  margin-bottom: 1.2rem;
}

.display-title em {
  font-style: italic;
  color: var(--purple);
}

.accent-text {
  font-family: var(--font-serif);
  font-size: 1rem;
  font-style: italic;
  color: var(--gold);
  margin-bottom: 2.5rem;
}

.stats {
  display: flex;
  gap: 2rem;
}

.stat { display: flex; flex-direction: column; gap: 0.2rem; }

.stat-num {
  font-family: var(--font-serif);
  font-size: 1.8rem;
  font-weight: 600;
  color: var(--purple);
  line-height: 1;
}

.stat-label {
  font-size: 0.7rem;
  letter-spacing: 0.08em;
  color: var(--text-muted-dark);
}

.text-col p {
  color: var(--text-muted-dark);
  margin-bottom: 1.1rem;
  line-height: 1.9;
}

.badges {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
  margin-top: 2rem;
  padding-top: 2rem;
  border-top: 1px solid rgba(7,4,14,0.08);
}

.badge {
  font-size: 0.72rem;
  letter-spacing: 0.05em;
  padding: 0.3em 0.9em;
  border-radius: 50px;
  border: 1px solid var(--gold);
  color: var(--gold);
  background: rgba(191, 78, 120, 0.06);
}

.bg-accent {
  position: absolute;
  top: -80px; right: -120px;
  width: 500px; height: 500px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(122, 27, 74, 0.08), transparent 70%);
  pointer-events: none;
}

@media (max-width: 900px) {
  .grid { grid-template-columns: 1fr; gap: 3rem; }
}

@media (max-width: 480px) {
  .stats { gap: 1.2rem; }
}
</style>
