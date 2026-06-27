<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)

const values = [
  { title: '上質な素材', desc: 'ストレッチ性・通気性に優れた国産・輸入生地を厳選' },
  { title: '美しいシルエット', desc: '体型に寄り添う立体裁断で、動きを美しく見せる' },
  { title: '豊富なデザイン', desc: 'シンプルから華やかなステージ向けまで幅広くラインナップ' },
]

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); observer.unobserve(e.target) } }),
    { threshold: 0.12 }
  )
  sectionRef.value?.querySelectorAll('.fade-in').forEach(el => observer.observe(el))
})
</script>

<template>
  <section id="concept" class="concept section" ref="sectionRef">
    <div class="container">
      <div class="grid">
        <div class="visual fade-in">
          <div class="morph-shape">
            <div class="inner-circle">
              <span class="icon">🍒</span>
            </div>
          </div>
          <div class="badge">Since 2024</div>
        </div>

        <div class="text fade-in" style="transition-delay: 0.15s">
          <p class="eyebrow">Our Concept</p>
          <h2 class="section-title">踊る喜びを、<br>美しく纏う</h2>

          <p class="lead">
            June BERRY は、舞台に立つ一人ひとりの「美しさ」と「動きやすさ」を
            同時に叶えるために生まれたレオタード専門店です。
          </p>
          <p>
            バレリーナ、体操選手、フィットネス愛好家―それぞれのシーンに合わせた
            素材選びと立体裁断により、着た瞬間から自信が生まれるウェアをお届けします。
          </p>
          <p>
            "June" は豊かさと美しさが溢れる季節を、"BERRY" は深みある色彩と
            愛らしさを表しています。どちらもあなたの個性を輝かせるための言葉です。
          </p>

          <ul class="values">
            <li v-for="v in values" :key="v.title">
              <span class="check">✦</span>
              <span><strong>{{ v.title }}</strong>：{{ v.desc }}</span>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.concept { background: var(--white); }

.grid {
  display: grid;
  grid-template-columns: 1fr 1.4fr;
  gap: 5rem;
  align-items: center;
}

.visual { position: relative; }

.morph-shape {
  width: 100%;
  max-width: 400px;
  aspect-ratio: 1;
  margin-inline: auto;
  border-radius: 40% 60% 60% 40% / 60% 40% 60% 40%;
  background: linear-gradient(135deg, var(--berry-pale) 0%, var(--pink) 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  animation: morph 8s ease-in-out infinite;
}

@keyframes morph {
  0%, 100% { border-radius: 40% 60% 60% 40% / 60% 40% 60% 40%; }
  33%       { border-radius: 60% 40% 40% 60% / 40% 60% 40% 60%; }
  66%       { border-radius: 50% 50% 30% 70% / 50% 70% 30% 50%; }
}

.inner-circle {
  width: 70%;
  aspect-ratio: 1;
  border-radius: 50%;
  background: var(--white);
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: var(--shadow-md);
}

.icon { font-size: 5rem; line-height: 1; }

.badge {
  position: absolute;
  bottom: 10%;
  right: 5%;
  background: var(--berry);
  color: var(--white);
  padding: 0.6em 1.2em;
  border-radius: 50px;
  font-size: 0.75rem;
  letter-spacing: 0.15em;
  box-shadow: var(--shadow-md);
}

.text p { color: var(--text-muted); margin-bottom: 1rem; }

.lead {
  font-size: 1.05rem !important;
  color: var(--text) !important;
  font-weight: 400;
  line-height: 1.9;
  margin-bottom: 1.5rem !important;
}

.values {
  margin-top: 2rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.values li { display: flex; gap: 0.8rem; align-items: flex-start; }

.check { color: var(--berry-light); font-size: 0.85rem; margin-top: 0.3rem; flex-shrink: 0; }

@media (max-width: 768px) {
  .grid { grid-template-columns: 1fr; gap: 3rem; }
  .visual { order: -1; }
  .morph-shape { max-width: 280px; }
}
</style>
