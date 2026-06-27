<script setup>
const INSTAGRAM_URL = 'https://www.instagram.com/juneberry_leotard/'

function scrollTo(id) {
  document.querySelector(id)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}

function particleStyle(n) {
  const x = ((n * 37 + 13) % 100)
  const y = ((n * 53 + 7) % 100)
  const size = 1 + (n % 3) * 1.5
  const delay = (n * 0.4) % 5
  const dur = 3 + (n % 4)
  return { left: `${x}%`, top: `${y}%`, width: `${size}px`, height: `${size}px`, animationDelay: `${delay}s`, animationDuration: `${dur}s` }
}
</script>

<template>
  <section class="hero">
    <div class="particles" aria-hidden="true">
      <span v-for="n in 24" :key="n" class="particle" :style="particleStyle(n)" />
    </div>
    <div class="orbs" aria-hidden="true">
      <div class="orb orb-1" /><div class="orb orb-2" /><div class="orb orb-3" />
    </div>

    <div class="content container">
      <div class="label-row">
        <span class="sport-badge">新体操専用</span>
        <span class="label-text">Rhythmic Gymnastics · Custom Order</span>
      </div>

      <h1 class="title">
        <span class="title-main">オーダーメイド</span>
        <span class="title-sub">新体操レオタード制作</span>
      </h1>

      <p class="tagline">一人ひとりの演技を引き立てる、<em>世界にひとつだけ</em>のレオタード</p>

      <p class="sub">
        デザインから縫製・装飾まで、すべて一人で丁寧に制作。<br>
        あなたの体型・演技・想いをヒアリングして、理想の一枚をお届けします。
      </p>

      <div class="cta">
        <a :href="INSTAGRAM_URL" target="_blank" rel="noopener noreferrer" class="btn btn-gold">
          Instagramで相談する
        </a>
        <button class="btn btn-outline-light" @click="scrollTo('#contact')">
          お問い合わせ・お見積り
        </button>
      </div>

      <div class="trust-row">
        <span class="trust-item"><strong>150枚以上</strong>制作実績</span>
        <span class="trust-sep">·</span>
        <span class="trust-item"><strong>ハンドメイド歴12年</strong></span>
        <span class="trust-sep">·</span>
        <span class="trust-item"><strong>全国送料無料</strong></span>
      </div>
    </div>

    <div class="scroll-hint" aria-hidden="true">
      <div class="scroll-line" />
      <span>SCROLL</span>
    </div>
  </section>

  <div class="marquee-strip" aria-hidden="true">
    <div class="marquee-track">
      <span v-for="n in 3" :key="n">
        オーダーメイド新体操レオタード &nbsp;◆&nbsp;
        JUNE BERRY &nbsp;◆&nbsp;
        フルオーダー / リメイク / 装飾追加 &nbsp;◆&nbsp;
        全国送料無料 &nbsp;◆&nbsp;
        制作実績150枚以上 &nbsp;◆&nbsp;
        丁寧なヒアリング &nbsp;◆&nbsp;
      </span>
    </div>
  </div>
</template>

<style scoped>
.hero {
  position: relative;
  min-height: 100svh;
  display: flex;
  align-items: center;
  overflow: hidden;
  background: var(--dark);
}

.particles { position: absolute; inset: 0; pointer-events: none; z-index: 1; }

.particle {
  position: absolute;
  border-radius: 50%;
  background: var(--gold);
  opacity: 0;
  animation: twinkle 4s ease-in-out infinite;
}

@keyframes twinkle {
  0%, 100% { opacity: 0; transform: scale(0.5); }
  50% { opacity: 0.6; transform: scale(1.2); }
}

.orbs { position: absolute; inset: 0; pointer-events: none; }

.orb { position: absolute; border-radius: 50%; filter: blur(80px); }

.orb-1 {
  width: 600px; height: 600px;
  background: radial-gradient(circle, rgba(122, 27, 74, 0.6), transparent 70%);
  top: -150px; right: -100px;
  animation: drift 12s ease-in-out infinite;
}

.orb-2 {
  width: 400px; height: 400px;
  background: radial-gradient(circle, rgba(191, 78, 120, 0.3), transparent 70%);
  bottom: -50px; left: -80px;
  animation: drift 10s ease-in-out infinite reverse;
}

.orb-3 {
  width: 300px; height: 300px;
  background: radial-gradient(circle, rgba(224, 139, 176, 0.35), transparent 70%);
  top: 30%; left: 20%;
  animation: drift 8s ease-in-out infinite;
}

@keyframes drift {
  0%, 100% { transform: translate(0, 0); }
  50% { transform: translate(30px, -30px); }
}

.content { position: relative; z-index: 2; padding-top: 7rem; }

.label-row {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;
  animation: fadeUp 1s var(--ease) 0.1s both;
  flex-wrap: wrap;
}

.sport-badge {
  background: var(--gold);
  color: var(--dark);
  font-size: 0.68rem;
  font-weight: 500;
  letter-spacing: 0.1em;
  padding: 0.35em 0.9em;
  border-radius: 50px;
}

.label-text {
  font-size: 0.72rem;
  letter-spacing: 0.2em;
  color: rgba(255,255,255,0.4);
}

.title {
  display: flex;
  flex-direction: column;
  font-family: var(--font-serif);
  font-weight: 300;
  line-height: 1.1;
  margin-bottom: 1.5rem;
}

.title-main {
  font-size: clamp(2rem, 6vw, 4rem);
  color: rgba(255,255,255,0.5);
  letter-spacing: 0.05em;
  animation: fadeUp 1s var(--ease) 0.2s both;
}

.title-sub {
  font-size: clamp(2.4rem, 7vw, 5rem);
  font-weight: 600;
  background: linear-gradient(135deg, var(--gold) 0%, var(--gold-light) 60%, var(--gold) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: fadeUp 1s var(--ease) 0.3s both;
}

.tagline {
  font-size: clamp(1rem, 2.5vw, 1.4rem);
  color: var(--champagne);
  opacity: 0.85;
  margin-bottom: 1rem;
  animation: fadeUp 1s var(--ease) 0.4s both;
  line-height: 1.6;
}

.tagline em {
  font-style: italic;
  color: var(--gold-light);
}

.sub {
  font-size: 0.9rem;
  color: rgba(255,255,255,0.5);
  line-height: 2;
  margin-bottom: 2.5rem;
  animation: fadeUp 1s var(--ease) 0.5s both;
}

.cta {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  margin-bottom: 2rem;
  animation: fadeUp 1s var(--ease) 0.6s both;
}

.trust-row {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  flex-wrap: wrap;
  animation: fadeUp 1s var(--ease) 0.7s both;
}

.trust-item {
  font-size: 0.78rem;
  color: rgba(255,255,255,0.45);
}

.trust-item strong { color: rgba(255,255,255,0.7); font-weight: 500; }

.trust-sep { color: rgba(255,255,255,0.2); }

.scroll-hint {
  position: absolute;
  bottom: 2.5rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.6rem;
  z-index: 2;
  animation: bounce 2.5s ease-in-out infinite;
}

.scroll-line {
  width: 1px; height: 52px;
  background: linear-gradient(to bottom, var(--gold), transparent);
}

.scroll-hint span { font-size: 0.6rem; letter-spacing: 0.3em; color: rgba(255,255,255,0.3); }

@keyframes bounce {
  0%, 100% { transform: translateX(-50%) translateY(0); }
  50% { transform: translateX(-50%) translateY(10px); }
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(32px); }
  to { opacity: 1; transform: translateY(0); }
}

.marquee-strip { background: var(--gold); overflow: hidden; padding: 0.9rem 0; }

.marquee-track {
  display: flex;
  width: max-content;
  animation: marquee 32s linear infinite;
  color: var(--dark);
  font-size: 0.72rem;
  font-weight: 500;
  letter-spacing: 0.12em;
  white-space: nowrap;
}

@keyframes marquee {
  from { transform: translateX(0); }
  to { transform: translateX(-33.333%); }
}

@media (max-width: 768px) {
  .cta { flex-direction: column; align-items: flex-start; }
  .scroll-hint { display: none; }
  .trust-row { gap: 0.5rem; }
}
</style>
