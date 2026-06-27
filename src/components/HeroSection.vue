<script setup>
function scrollTo(id) {
  document.querySelector(id)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}

function particleStyle(n) {
  const x = ((n * 37 + 13) % 100)
  const y = ((n * 53 + 7) % 100)
  const size = 1 + (n % 3) * 1.5
  const delay = (n * 0.4) % 5
  const dur = 3 + (n % 4)
  return {
    left: `${x}%`,
    top: `${y}%`,
    width: `${size}px`,
    height: `${size}px`,
    animationDelay: `${delay}s`,
    animationDuration: `${dur}s`,
  }
}
</script>

<template>
  <section class="hero">
    <!-- Sparkle particles -->
    <div class="particles" aria-hidden="true">
      <span v-for="n in 24" :key="n" class="particle" :style="particleStyle(n)" />
    </div>

    <!-- Gradient orbs -->
    <div class="orbs" aria-hidden="true">
      <div class="orb orb-1" />
      <div class="orb orb-2" />
      <div class="orb orb-3" />
    </div>

    <div class="content container">
      <div class="label-row">
        <span class="sport-badge">新体操専用</span>
        <span class="label-text">Rhythmic Gymnastics Leotard</span>
      </div>

      <h1 class="title">
        <span class="title-june">June</span>
        <span class="title-berry">BERRY</span>
      </h1>

      <p class="tagline">演技に魂を宿す、一枚。</p>

      <p class="sub">
        新体操の美しさと力強さを最大限に引き出すために。<br>
        上質な素材と繊細な手仕事が融合したレオタードをお届けします。
      </p>

      <div class="cta">
        <button class="btn btn-gold" @click="scrollTo('#products')">
          コレクションを見る
        </button>
        <button class="btn btn-outline-light" @click="scrollTo('#concept')">
          ブランドについて
        </button>
      </div>
    </div>

    <div class="scroll-hint" aria-hidden="true">
      <div class="scroll-line" />
      <span>SCROLL</span>
    </div>
  </section>

  <!-- Marquee strip -->
  <div class="marquee-strip" aria-hidden="true">
    <div class="marquee-track">
      <span v-for="n in 3" :key="n">
        新体操専用レオタード &nbsp;◆&nbsp;
        JUNE BERRY &nbsp;◆&nbsp;
        RHYTHMIC GYMNASTICS &nbsp;◆&nbsp;
        HANDCRAFTED QUALITY &nbsp;◆&nbsp;
        演技を彩る一枚 &nbsp;◆&nbsp;
        CUSTOM ORDER &nbsp;◆&nbsp;
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

/* Particles */
.particles {
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 1;
}

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

/* Orbs */
.orbs { position: absolute; inset: 0; pointer-events: none; }

.orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
}

.orb-1 {
  width: 600px; height: 600px;
  background: radial-gradient(circle, rgba(74, 27, 122, 0.6), transparent 70%);
  top: -150px; right: -100px;
  animation: drift 12s ease-in-out infinite;
}

.orb-2 {
  width: 400px; height: 400px;
  background: radial-gradient(circle, rgba(201, 162, 39, 0.2), transparent 70%);
  bottom: -50px; left: -80px;
  animation: drift 10s ease-in-out infinite reverse;
}

.orb-3 {
  width: 300px; height: 300px;
  background: radial-gradient(circle, rgba(194, 84, 122, 0.25), transparent 70%);
  top: 30%; left: 20%;
  animation: drift 8s ease-in-out infinite;
}

@keyframes drift {
  0%, 100% { transform: translate(0, 0); }
  50%       { transform: translate(30px, -30px); }
}

/* Content */
.content {
  position: relative;
  z-index: 2;
  padding-top: 7rem;
}

.label-row {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;
  animation: fadeUp 1s var(--ease) 0.1s both;
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
  letter-spacing: 0.25em;
  color: rgba(255,255,255,0.4);
  text-transform: uppercase;
}

.title {
  display: flex;
  flex-direction: column;
  font-family: var(--font-serif);
  font-weight: 300;
  line-height: 0.9;
  margin-bottom: 2rem;
}

.title-june {
  font-style: italic;
  font-size: clamp(5rem, 16vw, 11rem);
  color: var(--champagne);
  animation: fadeUp 1s var(--ease) 0.2s both;
}

.title-berry {
  font-size: clamp(2.2rem, 7.5vw, 5rem);
  font-weight: 600;
  letter-spacing: 0.2em;
  background: linear-gradient(135deg, var(--gold) 0%, var(--gold-light) 60%, var(--gold) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: fadeUp 1s var(--ease) 0.3s both;
}

.tagline {
  font-family: var(--font-serif);
  font-size: clamp(1.2rem, 3vw, 1.8rem);
  font-style: italic;
  color: var(--champagne);
  opacity: 0.8;
  margin-bottom: 1rem;
  animation: fadeUp 1s var(--ease) 0.4s both;
}

.sub {
  font-size: 0.9rem;
  color: rgba(255,255,255,0.5);
  line-height: 2;
  margin-bottom: 2.8rem;
  animation: fadeUp 1s var(--ease) 0.5s both;
}

.cta {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  animation: fadeUp 1s var(--ease) 0.6s both;
}

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
  width: 1px;
  height: 52px;
  background: linear-gradient(to bottom, var(--gold), transparent);
}

.scroll-hint span {
  font-size: 0.6rem;
  letter-spacing: 0.3em;
  color: rgba(255,255,255,0.3);
}

@keyframes bounce {
  0%, 100% { transform: translateX(-50%) translateY(0); }
  50%       { transform: translateX(-50%) translateY(10px); }
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(32px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* Marquee strip */
.marquee-strip {
  background: var(--gold);
  overflow: hidden;
  padding: 0.9rem 0;
}

.marquee-track {
  display: flex;
  width: max-content;
  animation: marquee 28s linear infinite;
  color: var(--dark);
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
  .label-row { flex-wrap: wrap; }
}
</style>
