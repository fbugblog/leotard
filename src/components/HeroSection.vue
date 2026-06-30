<script setup>
function scrollTo(id) {
  document.querySelector(id)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}

function sparkleStyle(n) {
  const x = ((n * 37 + 11) % 82) + 8
  const y = ((n * 59 + 7)  % 76) + 10
  const size = 0.5 + (n % 5) * 0.2
  const delay = (n * 0.47) % 4
  const dur = 2.8 + (n % 4) * 0.9
  return { left: `${x}%`, top: `${y}%`, fontSize: `${size}rem`, animationDelay: `${delay}s`, animationDuration: `${dur}s` }
}
</script>

<template>
  <section class="hero">
    <!-- Decorative blobs -->
    <div class="blob blob-1" aria-hidden="true" />
    <div class="blob blob-2" aria-hidden="true" />

    <!-- Background watermark -->
    <div class="bg-word" aria-hidden="true">GRACE</div>

    <!-- Floating sparkles -->
    <div class="sparkles" aria-hidden="true">
      <span v-for="n in 14" :key="n" class="sparkle" :style="sparkleStyle(n)">✦</span>
    </div>

    <div class="hero-grid container">
      <!-- Left: text -->
      <div class="hero-content">
        <div class="hero-badge">
          <span class="badge-dot" aria-hidden="true" />
          新体操 · ボディメイキング教室
        </div>

        <h1 class="hero-title">
          <span class="title-thin">美しい動きが、</span>
          <span class="title-bold">あなたを<em>変える</em>。</span>
        </h1>

        <p class="hero-desc">
          新体操の優雅さとボディメイキングを融合させた、<br>
          あなたの可能性を広げる新しいスタジオへ。
        </p>

        <div class="hero-cta">
          <button class="btn btn-primary" @click="scrollTo('#contact')">
            体験レッスンを予約
            <svg width="16" height="16" viewBox="0 0 16 16" fill="none" aria-hidden="true">
              <path d="M3 8h10M9 4l4 4-4 4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            </svg>
          </button>
          <button class="btn btn-outline" @click="scrollTo('#programs')">クラスを見る</button>
        </div>

        <div class="hero-stats">
          <div class="stat">
            <span class="stat-num">150<sup>+</sup></span>
            <span class="stat-label">在籍生徒数</span>
          </div>
          <div class="stat-line" aria-hidden="true" />
          <div class="stat">
            <span class="stat-num">15<span class="stat-unit">年</span></span>
            <span class="stat-label">指導経験</span>
          </div>
          <div class="stat-line" aria-hidden="true" />
          <div class="stat">
            <span class="stat-num">4<span class="stat-unit">種</span></span>
            <span class="stat-label">クラス区分</span>
          </div>
        </div>
      </div>

      <!-- Right: visual -->
      <div class="hero-visual" aria-hidden="true">
        <div class="vis-ring vis-ring-outer" />
        <div class="vis-ring vis-ring-mid" />
        <div class="vis-core">
          <span class="vis-label">DANCE</span>
          <span class="vis-emblem">G</span>
          <span class="vis-label">GRACE</span>
        </div>
        <div class="orbit-tag orbit-1">新体操</div>
        <div class="orbit-tag orbit-2">BODY MAKING</div>
        <div class="orbit-tag orbit-3">JUNIOR</div>
      </div>
    </div>

    <button class="scroll-down" @click="scrollTo('#concept')" aria-label="下へスクロール">
      <div class="scroll-line" />
      <span class="scroll-text">SCROLL</span>
    </button>
  </section>

  <!-- Marquee ticker -->
  <div class="marquee" aria-hidden="true">
    <div class="marquee-track">
      <span v-for="n in 4" :key="n">
        GRACE STUDIO &nbsp;♡&nbsp;
        新体操クラス &nbsp;·&nbsp;
        ボディメイキング &nbsp;·&nbsp;
        ジュニアコース &nbsp;·&nbsp;
        体験レッスン受付中 &nbsp;♡&nbsp;
        RHYTHMIC GYMNASTICS &nbsp;·&nbsp;
      </span>
    </div>
  </div>
</template>

<style scoped>
.hero {
  min-height: 100svh;
  display: flex;
  align-items: center;
  position: relative;
  overflow: hidden;
  background: var(--surface);
  padding-top: 5rem;
}

/* Blobs */
.blob {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  pointer-events: none;
}

.blob-1 {
  width: 600px; height: 600px;
  background: radial-gradient(circle, rgba(240, 78, 132, 0.12), transparent 70%);
  top: -150px; right: -100px;
  animation: drift 16s ease-in-out infinite;
}

.blob-2 {
  width: 400px; height: 400px;
  background: radial-gradient(circle, rgba(139, 92, 246, 0.1), transparent 70%);
  bottom: -80px; left: -80px;
  animation: drift 12s ease-in-out infinite reverse;
}

@keyframes drift {
  0%, 100% { transform: translate(0, 0); }
  50% { transform: translate(28px, -20px); }
}

/* Background word */
.bg-word {
  position: absolute;
  font-family: var(--font-display);
  font-size: clamp(8rem, 22vw, 20rem);
  font-weight: 800;
  color: transparent;
  -webkit-text-stroke: 1px rgba(240, 78, 132, 0.055);
  letter-spacing: -0.04em;
  top: 50%; left: 50%;
  transform: translate(-50%, -50%);
  pointer-events: none;
  white-space: nowrap;
  user-select: none;
  z-index: 0;
}

/* Sparkles */
.sparkles { position: absolute; inset: 0; pointer-events: none; z-index: 1; }

.sparkle {
  position: absolute;
  color: var(--pink-200);
  opacity: 0;
  animation: sparkle-float 3s ease-in-out infinite;
}

@keyframes sparkle-float {
  0%, 100% { opacity: 0; transform: translateY(0) scale(0.7); }
  45%       { opacity: 0.5; }
  50%       { opacity: 0.65; transform: translateY(-12px) scale(1.1); }
  55%       { opacity: 0.5; }
}

/* Hero grid */
.hero-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
  position: relative;
  z-index: 2;
  padding-block: 4rem;
}

/* Badge */
.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  font-family: var(--font-display);
  font-size: 0.7rem;
  font-weight: 500;
  letter-spacing: 0.1em;
  color: var(--text-mid);
  margin-bottom: 2rem;
  padding: 0.5em 1.1em 0.5em 0.8em;
  background: var(--pink-50);
  border-radius: 50px;
  border: 1px solid var(--pink-200);
  animation: fadeUp 0.8s var(--ease) 0.1s both;
}

.badge-dot {
  width: 6px; height: 6px;
  border-radius: 50%;
  background: var(--pink);
  flex-shrink: 0;
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.5); opacity: 0.6; }
}

/* Title */
.hero-title {
  display: flex;
  flex-direction: column;
  line-height: 1.1;
  margin-bottom: 1.8rem;
}

.title-thin {
  font-family: var(--font-serif);
  font-size: clamp(1.8rem, 4vw, 3rem);
  font-weight: 300;
  color: var(--text-mid);
  letter-spacing: 0.02em;
  animation: fadeUp 0.8s var(--ease) 0.2s both;
}

.title-bold {
  font-family: var(--font-serif);
  font-size: clamp(2.4rem, 5.5vw, 4.2rem);
  font-weight: 600;
  color: var(--text);
  letter-spacing: -0.01em;
  animation: fadeUp 0.8s var(--ease) 0.3s both;
}

.title-bold em {
  font-style: italic;
  background: linear-gradient(135deg, var(--pink) 0%, var(--violet) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* Desc */
.hero-desc {
  font-size: 0.95rem;
  color: var(--text-muted);
  line-height: 2;
  margin-bottom: 2.5rem;
  animation: fadeUp 0.8s var(--ease) 0.4s both;
}

/* CTA */
.hero-cta {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  margin-bottom: 3rem;
  animation: fadeUp 0.8s var(--ease) 0.5s both;
}

/* Stats */
.hero-stats {
  display: flex;
  align-items: center;
  gap: 2rem;
  padding-top: 2rem;
  border-top: 1px solid var(--border);
  animation: fadeUp 0.8s var(--ease) 0.6s both;
}

.stat { display: flex; flex-direction: column; gap: 0.2rem; }

.stat-num {
  font-family: var(--font-display);
  font-size: 1.8rem;
  font-weight: 700;
  color: var(--text);
  line-height: 1;
}

.stat-num sup, .stat-unit {
  font-size: 0.75em;
  font-weight: 500;
  color: var(--pink);
}

.stat-label {
  font-family: var(--font-display);
  font-size: 0.62rem;
  letter-spacing: 0.08em;
  color: var(--text-muted);
}

.stat-line {
  width: 1px; height: 40px;
  background: var(--border);
}

/* Visual */
.hero-visual {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 480px;
  animation: fadeUp 0.8s var(--ease) 0.3s both;
}

.vis-ring {
  position: absolute;
  border-radius: 50%;
}

.vis-ring-outer {
  width: 400px; height: 400px;
  border: 1.5px solid rgba(240, 78, 132, 0.15);
  animation: spin-cw 22s linear infinite;
}

.vis-ring-mid {
  width: 290px; height: 290px;
  border: 1.5px solid rgba(139, 92, 246, 0.18);
  animation: spin-ccw 15s linear infinite;
}

@keyframes spin-cw  { from { transform: rotate(0deg);   } to { transform: rotate(360deg);  } }
@keyframes spin-ccw { from { transform: rotate(0deg);   } to { transform: rotate(-360deg); } }

.vis-core {
  position: relative;
  z-index: 2;
  width: 200px; height: 200px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--pink) 0%, var(--violet) 100%);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.15rem;
  box-shadow: 0 20px 60px rgba(240, 78, 132, 0.35), 0 0 0 20px rgba(240, 78, 132, 0.06);
}

.vis-label {
  font-family: var(--font-display);
  font-size: 0.52rem;
  font-weight: 600;
  letter-spacing: 0.3em;
  color: rgba(255, 255, 255, 0.65);
  text-transform: uppercase;
}

.vis-emblem {
  font-family: var(--font-display);
  font-size: 4.5rem;
  font-weight: 700;
  color: var(--surface);
  line-height: 1;
}

/* Orbit tags */
.orbit-tag {
  position: absolute;
  font-family: var(--font-display);
  font-size: 0.6rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  padding: 0.35em 0.9em;
  border-radius: 50px;
  white-space: nowrap;
}

.orbit-1 {
  top: 10%; right: 14%;
  background: var(--pink-50);
  color: var(--pink-700);
  border: 1px solid var(--pink-200);
}

.orbit-2 {
  bottom: 22%; left: 2%;
  background: var(--violet-50);
  color: var(--violet-700);
  border: 1px solid var(--violet-200);
}

.orbit-3 {
  bottom: 10%; right: 6%;
  background: var(--surface);
  color: var(--text-mid);
  border: 1px solid var(--border-mid);
}

/* Scroll down */
.scroll-down {
  position: absolute;
  bottom: 2.5rem; left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  background: none;
  border: none;
  cursor: pointer;
  animation: scroll-bounce 2.5s ease-in-out infinite;
  z-index: 2;
}

.scroll-line {
  width: 1px; height: 48px;
  background: linear-gradient(to bottom, var(--pink), transparent);
  border-radius: 2px;
}

.scroll-text {
  font-family: var(--font-display);
  font-size: 0.52rem;
  font-weight: 600;
  letter-spacing: 0.3em;
  color: var(--text-muted);
}

@keyframes scroll-bounce {
  0%, 100% { transform: translateX(-50%) translateY(0); }
  50%       { transform: translateX(-50%) translateY(8px); }
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* Marquee */
.marquee {
  background: var(--pink);
  overflow: hidden;
  padding: 0.8rem 0;
}

.marquee-track {
  display: flex;
  width: max-content;
  animation: marquee 40s linear infinite;
  color: rgba(255, 255, 255, 0.9);
  font-family: var(--font-display);
  font-size: 0.68rem;
  font-weight: 500;
  letter-spacing: 0.1em;
  white-space: nowrap;
}

@keyframes marquee {
  from { transform: translateX(0); }
  to   { transform: translateX(-25%); }
}

/* Responsive */
@media (max-width: 900px) {
  .hero-grid { grid-template-columns: 1fr; gap: 3rem; }
  .hero-visual { height: 280px; order: -1; }
  .vis-ring-outer { width: 250px; height: 250px; }
  .vis-ring-mid   { width: 180px; height: 180px; }
  .vis-core { width: 130px; height: 130px; }
  .vis-emblem { font-size: 3rem; }
  .orbit-1 { top: 5%; right: 20%; }
  .orbit-2 { bottom: 15%; left: 10%; }
  .orbit-3 { bottom: 5%; right: 15%; }
}

@media (max-width: 600px) {
  .hero-cta { flex-direction: column; align-items: flex-start; }
  .hero-stats { gap: 1.2rem; }
  .scroll-down { display: none; }
}
</style>
