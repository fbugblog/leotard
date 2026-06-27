<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)

const testimonials = [
  {
    stars: 5,
    text: '「大会で着用したところ、審判の先生に衣装が素晴らしいと言っていただけました。スパンコールの輝きが照明に映えて、演技がより華やかに見えたと思います。」',
    name: 'M.K さん',
    meta: '新体操歴12年・高校生選手',
  },
  {
    stars: 5,
    text: '「チームの衣装をオーダーしました。全員のサイズが違う中でも完璧に仕上げていただき、統一感もあって本当に感動しました。来シーズンもお願いします！」',
    name: 'Y.T さん',
    meta: '新体操クラブコーチ・30代',
  },
  {
    stars: 5,
    text: '「練習用を5枚まとめて買いました。毎日洗っても型崩れせず、色も全然褪せない。これだけの品質でこの価格は驚きです。」',
    name: 'R.N さん',
    meta: '新体操クラブ保護者・40代',
  },
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
  <section class="testimonials section" ref="sectionRef">
    <div class="container">
      <span class="eyebrow center">Voice</span>
      <h2 class="display-title center">お客様の声</h2>

      <div class="grid">
        <blockquote
          v-for="(t, i) in testimonials"
          :key="t.name"
          class="card fade-in"
          :style="{ transitionDelay: `${i * 0.12}s` }"
        >
          <div class="quote-mark" aria-hidden="true">"</div>
          <div class="stars" :aria-label="`星${t.stars}つ`">
            <span v-for="n in t.stars" :key="n">★</span>
          </div>
          <p>{{ t.text }}</p>
          <footer>
            <div class="avatar">{{ t.name[0] }}</div>
            <div>
              <cite>{{ t.name }}</cite>
              <span>{{ t.meta }}</span>
            </div>
          </footer>
        </blockquote>
      </div>
    </div>
  </section>
</template>

<style scoped>
.testimonials {
  background: var(--white);
  border-top: 1px solid rgba(7,4,14,0.06);
}

.eyebrow { color: var(--gold); }

.display-title {
  color: var(--dark);
  margin-top: 0.5rem;
  margin-bottom: 3.5rem;
}

.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
}

.card {
  background: var(--cream);
  border-radius: var(--radius);
  padding: 2.5rem;
  position: relative;
  transition: transform var(--transition), box-shadow var(--transition), opacity 0.75s var(--ease);
  overflow: hidden;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-md);
}

.quote-mark {
  font-family: var(--font-serif);
  font-size: 5rem;
  line-height: 1;
  color: var(--gold);
  opacity: 0.2;
  position: absolute;
  top: 1rem;
  right: 1.5rem;
  font-weight: 600;
}

.stars {
  color: var(--gold);
  font-size: 0.85rem;
  letter-spacing: 0.1em;
  margin-bottom: 1rem;
}

.card p {
  font-size: 0.9rem;
  line-height: 1.9;
  color: var(--text-muted-dark);
  margin-bottom: 1.5rem;
  font-style: italic;
  position: relative;
  z-index: 1;
}

.card footer {
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.avatar {
  width: 38px; height: 38px;
  border-radius: 50%;
  background: var(--purple);
  color: var(--white);
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-serif);
  font-size: 1.1rem;
  font-weight: 600;
  flex-shrink: 0;
}

.card footer cite {
  font-size: 0.85rem;
  font-style: normal;
  color: var(--dark);
  font-weight: 500;
  display: block;
}

.card footer span {
  font-size: 0.75rem;
  color: var(--text-muted-dark);
}

@media (max-width: 900px) {
  .grid { grid-template-columns: 1fr 1fr; }
  .grid .card:last-child {
    grid-column: span 2;
    max-width: 480px;
    width: 100%;
    margin-inline: auto;
  }
}

@media (max-width: 600px) {
  .grid { grid-template-columns: 1fr; }
  .grid .card:last-child { grid-column: auto; max-width: none; }
}
</style>
