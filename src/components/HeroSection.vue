<script setup>
const INSTAGRAM_URL = 'https://www.instagram.com/juneberry_leotard/'

function scrollTo(id) {
  document.querySelector(id)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}

function sparkleStyle(n) {
  const x = ((n * 43 + 17) % 86) + 4
  const y = ((n * 61 + 11) % 80) + 6
  const size = 0.6 + (n % 4) * 0.35
  const delay = (n * 0.55) % 4.5
  const dur = 2.5 + (n % 4) * 1.1
  return {
    left: `${x}%`,
    top: `${y}%`,
    fontSize: `${size}rem`,
    animationDelay: `${delay}s`,
    animationDuration: `${dur}s`,
  }
}
</script>

<template>
  <section class="hero">
    <div class="blob blob-1" aria-hidden="true" />
    <div class="blob blob-2" aria-hidden="true" />
    <div class="blob blob-3" aria-hidden="true" />

    <div class="sparkles" aria-hidden="true">
      <span v-for="n in 18" :key="n" class="sparkle" :style="sparkleStyle(n)">✦</span>
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
        <a :href="INSTAGRAM_URL" target="_blank" rel="noopener noreferrer" class="btn btn-pink">
          Instagramで相談する
        </a>
        <button class="btn btn-outline-pink" @click="scrollTo('#contact')">
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
        オーダーメイド新体操レオタード &nbsp;♡&nbsp;
        JUNE Berry &nbsp;♡&nbsp;
        フルオーダー / リメイク / 装飾追加 &nbsp;♡&nbsp;
        全国送料無料 &nbsp;♡&nbsp;
        制作実績150枚以上 &nbsp;♡&nbsp;
        丁寧なヒアリング &nbsp;♡&nbsp;
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
  background: linear-gradient(160deg, #fff8fb 0%, #fde4f2 45%, #fdf2f8 100%);
}

/* Blobs */
.blob {
  position: absolute;
  border-radius: 50%;
  filter: blur(72px);
  pointer-events: none;
}

.blob-1 {
  width: 580px; height: 580px;
  background: radial-gradient(circle, rgba(232, 130, 175, 0.32), transparent 70%);
  top: -140px; right: -90px;
  animation: drift 14s ease-in-out infinite;
}

.blob-2 {
  width: 380px; height: 380px;
  background: radial-gradient(circle, rgba(210, 148, 225, 0.25), transparent 70%);
  bottom: -60px; left: -60px;
  animation: drift 11s ease-in-out infinite reverse;
}

.blob-3 {
  width: 280px; height: 280px;
  background: radial-gradient(circle, rgba(255, 176, 215, 0.38), transparent 70%);
  top: 38%; left: 18%;
  animation: drift 9s ease-in-out infinite;
}

@keyframes drift {
  0%, 100% { transform: translate(0, 0); }
  50% { transform: translate(22px, -22px); }
}

/* Sparkles */
.sparkles { position: absolute; inset: 0; pointer-events: none; z-index: 1; }

.sparkle {
  position: absolute;
  color: #E08BB0;
  opacity: 0;
  animation: sparkle-float 3s ease-in-out infinite;
}

@keyframes sparkle-float {
  0%, 100% { opacity: 0; transform: translateY(0) scale(0.6); }
  40%       { opacity: 0.55; }
  50%       { opacity: 0.65; transform: translateY(-14px) scale(1.1); }
  60%       { opacity: 0.55; }
}

/* Content */
.content { position: relative; z-index: 2; padding-top: 7rem; }

.label-row {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;
  animation: fadeUp 0.9s var(--ease) 0.1s both;
  flex-wrap: wrap;
}

.sport-badge {
  background: var(--gold);
  color: var(--white);
  font-size: 0.68rem;
  font-weight: 600;
  letter-spacing: 0.1em;
  padding: 0.35em 1em;
  border-radius: 50px;
  box-shadow: 0 3px 12px rgba(191, 78, 120, 0.25);
}

.label-text {
  font-size: 0.72rem;
  letter-spacing: 0.18em;
  color: rgba(90, 30, 60, 0.4);
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
  color: rgba(80, 25, 50, 0.4);
  letter-spacing: 0.05em;
  animation: fadeUp 0.9s var(--ease) 0.2s both;
}

.title-sub {
  font-size: clamp(2.4rem, 7vw, 5rem);
  font-weight: 600;
  background: linear-gradient(135deg, #BF4E78 0%, #E08BB0 55%, #BF4E78 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: fadeUp 0.9s var(--ease) 0.3s both;
}

.tagline {
  font-size: clamp(1rem, 2.5vw, 1.3rem);
  color: #5A2840;
  opacity: 0.8;
  margin-bottom: 1rem;
  animation: fadeUp 0.9s var(--ease) 0.4s both;
  line-height: 1.7;
}

.tagline em {
  font-style: italic;
  color: var(--gold);
}

.sub {
  font-size: 0.9rem;
  color: rgba(90, 40, 65, 0.5);
  line-height: 2;
  margin-bottom: 2.5rem;
  animation: fadeUp 0.9s var(--ease) 0.5s both;
}

.cta {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  margin-bottom: 2rem;
  animation: fadeUp 0.9s var(--ease) 0.6s both;
}

.btn-pink {
  background: linear-gradient(135deg, #BF4E78, #E08BB0);
  color: var(--white);
  border-color: transparent;
  box-shadow: 0 6px 24px rgba(191, 78, 120, 0.3);
}
.btn-pink:hover {
  box-shadow: 0 10px 32px rgba(191, 78, 120, 0.45);
}

.btn-outline-pink {
  background: transparent;
  color: var(--gold);
  border-color: var(--gold);
}
.btn-outline-pink:hover {
  background: rgba(191, 78, 120, 0.07);
}

.trust-row {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  flex-wrap: wrap;
  animation: fadeUp 0.9s var(--ease) 0.7s both;
}

.trust-item {
  font-size: 0.78rem;
  color: rgba(90, 40, 65, 0.45);
}

.trust-item strong {
  color: rgba(90, 40, 65, 0.72);
  font-weight: 600;
}

.trust-sep { color: rgba(191, 78, 120, 0.3); }

/* Scroll hint */
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

.scroll-hint span {
  font-size: 0.6rem;
  letter-spacing: 0.3em;
  color: rgba(191, 78, 120, 0.4);
}

@keyframes bounce {
  0%, 100% { transform: translateX(-50%) translateY(0); }
  50%       { transform: translateX(-50%) translateY(10px); }
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(28px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* Marquee */
.marquee-strip {
  background: linear-gradient(90deg, #E098BC, #EDAFD0, #E098BC);
  overflow: hidden;
  padding: 0.85rem 0;
}

.marquee-track {
  display: flex;
  width: max-content;
  animation: marquee 32s linear infinite;
  color: #fff;
  font-size: 0.72rem;
  font-weight: 500;
  letter-spacing: 0.12em;
  white-space: nowrap;
}

@keyframes marquee {
  from { transform: translateX(0); }
  to   { transform: translateX(-33.333%); }
}

@media (max-width: 768px) {
  .cta { flex-direction: column; align-items: flex-start; }
  .scroll-hint { display: none; }
  .trust-row { gap: 0.5rem; }
}
</style>
