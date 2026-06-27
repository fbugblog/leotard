<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)

const testimonials = [
  {
    stars: 5,
    text: '「レッスンで着るたびに先生や生徒さんに褒めてもらえます。フィット感が素晴らしく、動いても形が崩れない！」',
    name: 'M.K さん',
    meta: '（バレエ歴15年・30代）',
  },
  {
    stars: 5,
    text: '「試合用にオーダーしました。希望通りのデザインで仕上がり、娘もとても喜んでいます。また注文したいです。」',
    name: 'T.S さん',
    meta: '（体操クラブ保護者・40代）',
  },
  {
    stars: 5,
    text: '「サイズについて相談したらとても丁寧に答えてくださいました。商品の品質はもちろん、接客も満点です。」',
    name: 'A.Y さん',
    meta: '（フィットネスインストラクター・20代）',
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
  <section class="testimonials section" ref="sectionRef">
    <div class="container">
      <p class="eyebrow center light">Voice</p>
      <h2 class="section-title center light">お客様の声</h2>

      <div class="grid">
        <blockquote
          v-for="(t, i) in testimonials"
          :key="t.name"
          class="card fade-in"
          :style="{ transitionDelay: `${i * 0.12}s` }"
        >
          <div class="stars" :aria-label="`星${t.stars}つ`">
            <span v-for="n in t.stars" :key="n">★</span>
          </div>
          <p>{{ t.text }}</p>
          <footer>
            <cite>{{ t.name }} <span>{{ t.meta }}</span></cite>
          </footer>
        </blockquote>
      </div>
    </div>
  </section>
</template>

<style scoped>
.testimonials {
  background: linear-gradient(135deg, var(--berry) 0%, var(--berry-light) 100%);
}

.eyebrow.light { color: var(--pink); }
.section-title.light { color: var(--white); }

.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.card {
  background: rgba(255, 255, 255, 0.12);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: var(--radius);
  padding: 2rem;
  transition: transform var(--transition), background var(--transition), opacity 0.7s ease;
}

.card:hover {
  transform: translateY(-4px);
  background: rgba(255, 255, 255, 0.18);
}

.stars {
  color: var(--gold);
  font-size: 0.9rem;
  letter-spacing: 0.1em;
  margin-bottom: 1rem;
}

.card p {
  font-size: 0.9rem;
  line-height: 1.9;
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: 1.2rem;
  font-style: italic;
}

.card footer cite {
  font-size: 0.8rem;
  font-style: normal;
  color: rgba(255, 255, 255, 0.75);
  font-weight: 500;
}

.card footer cite span {
  font-weight: 300;
  opacity: 0.8;
  font-size: 0.75rem;
  display: block;
}

@media (max-width: 1024px) {
  .grid { grid-template-columns: repeat(2, 1fr); }
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
