<script setup>
import { ref, onMounted } from 'vue'

const sectionRef = ref(null)
const openIndex = ref(null)

function toggle(i) {
  openIndex.value = openIndex.value === i ? null : i
}

const faqs = [
  {
    q: '納期はどのくらいかかりますか？',
    a: 'フルオーダーの場合、ヒアリングから完成まで通常4〜8週間です。大会の日程が決まっている場合は、早めにご相談ください。リメイク・装飾追加は内容によって異なります。',
  },
  {
    q: 'サイズはどのように決めますか？',
    a: 'お体の採寸箇所をご案内します。既成サイズへの近似でも、完全カスタムサイズにも対応しています。ジュニア（90cm〜）から大人まで幅広く対応可能です。',
  },
  {
    q: 'デザインの参考画像を持ち込めますか？',
    a: 'もちろんです。InstagramやPinterestで見つけた画像、大会で見た衣装の写真など、何でもお送りください。イメージを共有していただくほど、理想に近い仕上がりになります。',
  },
  {
    q: '既存のレオタードのリメイクはできますか？',
    a: 'はい、対応しています。補修・装飾追加・スカート取り付け・カラー変更など、まずは現状をご連絡ください。状態を確認してからお見積りします。',
  },
  {
    q: '全国への発送はできますか？',
    a: 'はい、日本全国に対応しています。送料は完全無料です。大切なレオタードが傷まないよう、専用ボックスで丁寧に梱包してお届けします。',
  },
  {
    q: '洗濯方法を教えてください。',
    a: '手洗い（30℃以下、中性洗剤）を推奨しています。洗濯ネットに入れての洗濯機使用も可能ですが、ストーン装飾がある場合は特に手洗いをおすすめします。乾燥機の使用はお避けください。',
  },
  {
    q: '支払い方法は何がありますか？',
    a: '銀行振込・PayPay・クレジットカード（オンライン決済）に対応しています。制作前に半額、完成時に残額をお支払いいただく形になります。',
  },
]

onMounted(() => {
  const obs = new IntersectionObserver(
    (es) => es.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); obs.unobserve(e.target) } }),
    { threshold: 0.05 }
  )
  sectionRef.value?.querySelectorAll('.fade-in').forEach(el => obs.observe(el))
})
</script>

<template>
  <section id="faq" class="faq section" ref="sectionRef">
    <div class="container">
      <div class="header fade-in">
        <span class="eyebrow">FAQ</span>
        <h2 class="display-title">よくある質問</h2>
      </div>

      <div class="list">
        <div
          v-for="(faq, i) in faqs"
          :key="i"
          class="item fade-in"
          :class="{ open: openIndex === i }"
          :style="{ transitionDelay: `${i * 0.06}s` }"
        >
          <button class="item__q" @click="toggle(i)" :aria-expanded="openIndex === i">
            <span>{{ faq.q }}</span>
            <span class="item__icon" aria-hidden="true">{{ openIndex === i ? '−' : '+' }}</span>
          </button>
          <div class="item__a" v-show="openIndex === i">
            <p>{{ faq.a }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.faq {
  background: var(--white);
  border-top: 1px solid rgba(7,4,14,0.06);
}

.header { margin-bottom: 3rem; }

.header .display-title { color: var(--dark); margin-top: 0.5rem; }

.list {
  max-width: 720px;
  display: flex;
  flex-direction: column;
  gap: 0;
}

.item {
  border-bottom: 1px solid rgba(7,4,14,0.08);
  transition: opacity 0.75s var(--ease);
}

.item:first-child { border-top: 1px solid rgba(7,4,14,0.08); }

.item__q {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  padding: 1.4rem 0;
  background: none;
  border: none;
  cursor: pointer;
  text-align: left;
  font-family: var(--font-sans);
  font-size: 0.95rem;
  font-weight: 500;
  color: var(--dark);
  transition: color var(--transition);
}

.item__q:hover { color: var(--gold); }

.item.open .item__q { color: var(--gold); }

.item__icon {
  font-size: 1.4rem;
  font-weight: 300;
  color: var(--gold);
  flex-shrink: 0;
  line-height: 1;
  width: 24px;
  text-align: center;
}

.item__a {
  padding-bottom: 1.4rem;
}

.item__a p {
  font-size: 0.875rem;
  color: var(--text-muted-dark);
  line-height: 1.9;
}
</style>
