<script setup>
import { ref, onMounted } from 'vue'

const INSTAGRAM_URL = 'https://www.instagram.com/juneberry_leotard/'

const sectionRef = ref(null)

const items = [
  {
    tag: 'Full Order',
    title: 'フルオーダー',
    desc: 'デザイン・生地・カラー・装飾・シルエットすべてをゼロから制作。大会・発表会・チームウェアに対応。照明に映えるスパンコールやラインストーンの装飾も込み込みでご相談いただけます。',
    features: ['デザイン完全自由', 'ストーン・スパンコール装飾', 'カスタムサイズ対応', 'チーム一括注文可'],
    accent: '#7A1B4A',
    accentLight: 'rgba(122,27,74,0.08)',
  },
  {
    tag: 'Remake',
    title: 'リメイク',
    desc: '今あるレオタードをより美しく。傷んだ部分の補修・色あせた箇所のリカバリー・装飾の追加や変更など、思い出のレオタードをよみがえらせます。',
    features: ['補修・修繕', '装飾追加・変更', '部分カラー変更', 'サイズ調整'],
    accent: '#BF4E78',
    accentLight: 'rgba(191,78,120,0.08)',
  },
  {
    tag: 'Practice',
    title: '練習用レオタード',
    desc: '毎日のレッスンに寄り添う実用的な一枚。伸縮性と耐久性を重視し、洗濯を繰り返しても型崩れしません。シンプルなデザインでも丁寧な縫製が光ります。',
    features: ['速乾・型崩れしにくい', '豊富なカラー展開', 'ジュニア〜大人まで', '1枚から注文可'],
    accent: '#C2547A',
    accentLight: 'rgba(194,84,122,0.08)',
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
  <section id="gallery" class="gallery section" ref="sectionRef">
    <div class="container">
      <div class="section-header fade-in">
        <span class="eyebrow">Gallery &amp; Menu</span>
        <h2 class="display-title">制作メニュー</h2>
        <p class="section-sub">
          フルオーダーからリメイクまで。作品はInstagramで随時公開中です。
        </p>
      </div>

      <div class="list">
        <article
          v-for="(item, i) in items"
          :key="item.tag"
          class="item fade-in"
          :style="{ transitionDelay: `${i * 0.12}s`, '--accent': item.accent, '--accent-bg': item.accentLight }"
        >
          <div class="item__accent-bar" />
          <div class="item__inner">
            <div class="item__header">
              <span class="item__tag">{{ item.tag }}</span>
              <h3 class="item__title">{{ item.title }}</h3>
            </div>
            <p class="item__desc">{{ item.desc }}</p>
            <ul class="item__features">
              <li v-for="f in item.features" :key="f">
                <span class="check">✓</span>{{ f }}
              </li>
            </ul>
          </div>
        </article>
      </div>

      <div class="instagram-cta fade-in">
        <p>実際の作品をもっと見る</p>
        <a :href="INSTAGRAM_URL" target="_blank" rel="noopener noreferrer" class="btn btn-outline-dark">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" aria-hidden="true">
            <rect x="2" y="2" width="20" height="20" rx="5" ry="5"/>
            <circle cx="12" cy="12" r="4"/>
            <circle cx="17.5" cy="6.5" r="0.5" fill="currentColor" stroke="none"/>
          </svg>
          Instagramで作品を見る
        </a>
      </div>
    </div>
  </section>
</template>

<style scoped>
.gallery { background: var(--white); }

.section-header { margin-bottom: 3.5rem; }

.section-header .display-title { margin-top: 0.5rem; color: var(--dark); }

.section-sub {
  margin-top: 0.8rem;
  font-size: 0.9rem;
  color: var(--text-muted-dark);
  line-height: 1.8;
}

.list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  margin-bottom: 3rem;
}

.item {
  background: var(--cream);
  border-radius: var(--radius);
  position: relative;
  overflow: hidden;
  transition: transform var(--transition), box-shadow var(--transition), opacity 0.75s var(--ease);
}

.item:hover {
  transform: translateY(-6px);
  box-shadow: var(--shadow-md);
}

.item__accent-bar {
  height: 4px;
  background: var(--accent);
  border-radius: 2px 2px 0 0;
}

.item__inner { padding: 2rem; }

.item__header { margin-bottom: 1rem; }

.item__tag {
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  font-weight: 500;
  color: var(--accent);
  display: block;
  margin-bottom: 0.4rem;
}

.item__title {
  font-family: var(--font-serif);
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--dark);
}

.item__desc {
  font-size: 0.875rem;
  color: var(--text-muted-dark);
  line-height: 1.9;
  margin-bottom: 1.5rem;
}

.item__features {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
}

.item__features li {
  font-size: 0.8rem;
  color: var(--text-muted-dark);
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.check {
  color: var(--accent);
  font-weight: 600;
  flex-shrink: 0;
}

.instagram-cta {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  padding: 2rem;
  background: var(--cream);
  border-radius: var(--radius);
  flex-wrap: wrap;
}

.instagram-cta p {
  font-size: 0.9rem;
  color: var(--text-muted-dark);
  flex: 1;
  min-width: 200px;
}

.btn-outline-dark {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75em 1.6em;
  border: 1.5px solid var(--dark);
  border-radius: 50px;
  font-size: 0.85rem;
  font-weight: 500;
  color: var(--dark);
  letter-spacing: 0.05em;
  text-decoration: none;
  transition: background var(--transition), color var(--transition);
  white-space: nowrap;
}

.btn-outline-dark:hover {
  background: var(--dark);
  color: var(--white);
}

@media (max-width: 900px) {
  .list { grid-template-columns: 1fr; }
}
</style>
