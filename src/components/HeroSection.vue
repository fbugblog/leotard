<script setup>
function scrollTo(id) {
  document.querySelector(id)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}
</script>

<template>
  <section class="hero">
    <!-- Decorative background blobs -->
    <div class="hero-bg" aria-hidden="true">
      <div class="blob blob-1"></div>
      <div class="blob blob-2"></div>
      <div class="blob blob-3"></div>
    </div>

    <div class="hero-content container">
      <p class="hero-eyebrow">レオタード専門店</p>

      <h1 class="hero-title">
        <span class="june">June</span>
        <span class="berry">BERRY</span>
      </h1>

      <p class="hero-tagline">纏うほどに、輝きが増す。</p>

      <p class="hero-sub">
        バレエ・体操・フィットネス専用レオタード<br>
        上質な素材と繊細なデザインで、あなたを彩ります。
      </p>

      <div class="hero-cta">
        <button class="btn btn-primary" @click="scrollTo('#products')">
          コレクションを見る
        </button>
        <button class="btn btn-outline" @click="scrollTo('#concept')">
          ブランドについて
        </button>
      </div>
    </div>

    <div class="hero-scroll" aria-hidden="true">
      <span>SCROLL</span>
      <div class="scroll-line"></div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  position: relative;
  min-height: 100svh;
  display: flex;
  align-items: center;
  overflow: hidden;
  background: linear-gradient(135deg, var(--cream) 0%, var(--ivory) 50%, #F5E0EE 100%);
}

.hero-bg {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.blob {
  position: absolute;
  border-radius: 50%;
  background: radial-gradient(circle, var(--pink) 0%, transparent 70%);
}

.blob-1 {
  width: 800px; height: 800px;
  top: -200px; right: -200px;
  opacity: 0.35;
  animation: float 8s ease-in-out infinite;
}

.blob-2 {
  width: 500px; height: 500px;
  bottom: -100px; left: -100px;
  opacity: 0.2;
  animation: float 10s ease-in-out infinite reverse;
}

.blob-3 {
  width: 300px; height: 300px;
  top: 40%; left: 30%;
  opacity: 0.15;
  animation: float 6s ease-in-out infinite;
}

@keyframes float {
  0%, 100% { transform: translate(0, 0) scale(1); }
  50% { transform: translate(20px, -20px) scale(1.05); }
}

.hero-content {
  position: relative;
  z-index: 1;
  padding-top: 6rem;
  max-width: 700px;
}

.hero-eyebrow {
  font-size: 0.78rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--berry-light);
  margin-bottom: 1rem;
}

.hero-title {
  display: flex;
  flex-direction: column;
  line-height: 1;
  margin-bottom: 1.5rem;
  font-family: var(--font-serif);
  font-weight: 300;
}

.june {
  font-style: italic;
  font-size: clamp(4rem, 14vw, 9rem);
  color: var(--berry);
  animation: slideUp 0.9s var(--ease) both;
}

.berry {
  font-size: clamp(2rem, 7vw, 4.5rem);
  font-weight: 600;
  letter-spacing: 0.18em;
  color: var(--berry-light);
  animation: slideUp 0.9s var(--ease) 0.1s both;
}

@keyframes slideUp {
  from { opacity: 0; transform: translateY(30px); }
  to   { opacity: 1; transform: translateY(0); }
}

.hero-tagline {
  font-family: var(--font-serif);
  font-size: clamp(1.1rem, 2.5vw, 1.5rem);
  font-style: italic;
  color: var(--text-muted);
  margin-bottom: 1rem;
  animation: slideUp 0.9s var(--ease) 0.2s both;
}

.hero-sub {
  font-size: 0.95rem;
  color: var(--text-muted);
  line-height: 2;
  margin-bottom: 2.5rem;
  animation: slideUp 0.9s var(--ease) 0.3s both;
}

.hero-cta {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  animation: slideUp 0.9s var(--ease) 0.4s both;
}

.hero-scroll {
  position: absolute;
  bottom: 2.5rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  color: var(--text-muted);
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  animation: bounce 2s ease-in-out infinite;
}

.scroll-line {
  width: 1px;
  height: 48px;
  background: linear-gradient(to bottom, var(--berry-light), transparent);
}

@keyframes bounce {
  0%, 100% { transform: translateX(-50%) translateY(0); }
  50%       { transform: translateX(-50%) translateY(8px); }
}

@media (max-width: 768px) {
  .hero-cta { flex-direction: column; align-items: flex-start; }
  .hero-scroll { display: none; }
}
</style>
