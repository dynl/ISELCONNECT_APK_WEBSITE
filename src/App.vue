<script setup>
// Vite resolves "@" to /src by default (create-vue / Vue CLI projects).
// If your project has no "@" alias, use a relative path instead,
// e.g. '../assets/ISELCONNECT.png'
import logo from './assets/ISELCONNECT.png'

const steps = [
  {
    title: 'Download the file',
    body: 'Tap the yellow button. Your browser may ask you to confirm the download.',
  },
  {
    title: 'Open the .apk',
    body: 'Find it in your notification panel or the Downloads folder.',
  },
  {
    title: 'Allow unknown sources',
    body: 'If a security warning appears, tap Settings and turn on Allow from this source.',
  },
  {
    title: 'Install and log in',
    body: 'Tap Install, then open ISELCONNECT and sign in.',
  },
]
</script>

<template>
  <main class="page">
    <div class="shell">
      <!-- Brand + download -->
      <section class="panel panel-brand" aria-labelledby="app-title">
        <svg class="grid-lines" viewBox="0 0 400 400" preserveAspectRatio="xMidYMid slice" aria-hidden="true">
          <path d="M-20 90 Q 200 40 420 110" />
          <path d="M-20 130 Q 200 80 420 150" />
          <path d="M-20 170 Q 200 120 420 190" />
          <line x1="70" y1="60" x2="70" y2="400" />
          <line x1="330" y1="80" x2="330" y2="400" />
        </svg>

        <div class="brand-content">
          <div class="logo-card">
            <img :src="logo" alt="" class="logo" />
          </div>

          <!-- Kept for screen readers and SEO; the logo already shows the name -->
          <h1 id="app-title" class="sr-only">ISELCONNECT</h1>
          <p class="subtitle">
            The official portal for residents and linemen. Report issues, check
            your account status, and stay connected.
          </p>
        </div>

        <div class="download">
          <a href="/iselconnect.apk" download="ISELCONNECT.apk" class="btn">
            <svg viewBox="0 0 24 24" width="22" height="22" aria-hidden="true">
              <path
                d="M12 3v12m0 0-4.5-4.5M12 15l4.5-4.5M4 20h16"
                fill="none"
                stroke="currentColor"
                stroke-width="2.4"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
            Download for Android
          </a>
          <p class="meta">Version 1.0 · .apk file · Android only</p>
        </div>
      </section>

      <!-- Install guide -->
      <section class="panel panel-steps" aria-labelledby="steps-title">
        <h2 id="steps-title" class="steps-title">Install in four steps</h2>

        <ol class="steps">
          <li v-for="(step, i) in steps" :key="step.title" class="step">
            <span class="step-num" aria-hidden="true">{{ i + 1 }}</span>
            <div class="step-text">
              <h3>{{ step.title }}</h3>
              <p>{{ step.body }}</p>
            </div>
          </li>
        </ol>

        <aside class="note">
          <strong>Why the warning?</strong>
          ISELCONNECT is installed directly from this page, not the Play Store,
          so Android asks you to confirm. Only install files from a source you trust.
        </aside>
      </section>
    </div>
  </main>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,600;12..96,800&family=Public+Sans:wght@400;500;600&display=swap');

/* Tokens: white, blue, yellow */
.page {
  --blue: #1b0b8c;
  --blue-deep: #12065f;
  --yellow: #ffde59;
  --yellow-deep: #e6c33d;
  --yellow-tint: #fff8d6;
  --white: #ffffff;
  --page-bg: #f5f4fc;
  --text: #22204a;
  --muted: #5d5a86;
  --line: #dedcf0;
  --display: 'Bricolage Grotesque', 'Segoe UI', system-ui, sans-serif;
  --body: 'Public Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;

  min-height: 100vh;
  min-height: 100dvh;
  display: flex;
  align-items: center;
  justify-content: center;
  box-sizing: border-box;
  padding: 16px;
  background: var(--page-bg);
  font-family: var(--body);
  color: var(--text);
  -webkit-text-size-adjust: 100%;
  text-align: left;
}
.page *,
.page *::before,
.page *::after {
  box-sizing: border-box;
}

.shell {
  display: grid;
  grid-template-columns: minmax(0, 1fr);
  width: 100%;
  max-width: 560px;
  border-radius: 20px;
  overflow: hidden;
  background: var(--white);
  box-shadow: 0 24px 60px -24px rgba(27, 11, 140, 0.4);
}

.panel {
  min-width: 0;
  padding: 28px 20px;
}

/* Brand panel */
.panel-brand {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 32px;
  background: linear-gradient(160deg, var(--blue) 0%, var(--blue-deep) 100%);
  color: var(--white);
  overflow: hidden;
}

.grid-lines {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}
.grid-lines path,
.grid-lines line {
  fill: none;
  stroke: rgba(255, 222, 89, 0.16);
  stroke-width: 1.5;
}

.brand-content,
.download {
  position: relative;
}

/* White card keeps the logo's dark-blue lettering visible on the blue panel */
.logo-card {
  width: 100%;
  max-width: 360px;
  margin-bottom: 24px;
  padding: clamp(18px, 5vw, 28px);
  border-radius: 20px;
  background: var(--white);
  box-shadow: 0 0 0 4px var(--yellow), 0 14px 30px -12px rgba(0, 0, 0, 0.45);
}
.logo {
  display: block;
  width: 100%;
  height: auto;
  max-height: 220px;
  object-fit: contain;
}

.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

.subtitle {
  margin: 0;
  max-width: 36ch;
  font-size: 1rem;
  line-height: 1.6;
  color: #d4d0f5;
}

/* Download button */
.btn {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  width: 100%;
  min-height: 56px;
  padding: 16px 20px;
  border-radius: 12px;
  background: var(--yellow);
  color: var(--blue);
  font-family: var(--display);
  font-size: 1.1rem;
  font-weight: 800;
  text-decoration: none;
  box-shadow: 0 6px 0 var(--yellow-deep);
  transition: transform 0.12s ease, box-shadow 0.12s ease;
  -webkit-tap-highlight-color: transparent;
}
.btn:hover {
  transform: translateY(2px);
  box-shadow: 0 4px 0 var(--yellow-deep);
}
.btn:active {
  transform: translateY(6px);
  box-shadow: 0 0 0 var(--yellow-deep);
}
.btn:focus-visible {
  outline: 3px solid var(--white);
  outline-offset: 4px;
}

.meta {
  margin: 20px 0 0;
  font-size: 0.85rem;
  color: #b9b4ea;
  text-align: center;
}

/* Steps panel */
.steps-title {
  margin: 0 0 22px;
  font-family: var(--display);
  font-size: 1.35rem;
  font-weight: 800;
  color: var(--blue);
}

.steps {
  position: relative;
  margin: 0;
  padding: 0;
  list-style: none;
}
.steps::before {
  content: '';
  position: absolute;
  left: 15px;
  top: 16px;
  bottom: 16px;
  width: 2px;
  background: var(--line);
}

.step {
  position: relative;
  display: flex;
  gap: 14px;
  padding-bottom: 20px;
}
.step:last-child {
  padding-bottom: 0;
}

.step-num {
  position: relative;
  flex: none;
  display: grid;
  place-items: center;
  width: 32px;
  height: 32px;
  border-radius: 50%;
  background: var(--blue);
  color: var(--yellow);
  font-family: var(--display);
  font-size: 0.95rem;
  font-weight: 800;
  box-shadow: 0 0 0 4px var(--white);
}

.step-text {
  min-width: 0;
}
.step h3 {
  margin: 4px 0 4px;
  font-size: 1rem;
  font-weight: 600;
  color: var(--blue);
}
.step p {
  margin: 0;
  max-width: 46ch;
  font-size: 0.94rem;
  line-height: 1.55;
  color: var(--muted);
}

/* Safety note */
.note {
  margin-top: 26px;
  padding: 14px 16px;
  border-left: 4px solid var(--yellow);
  border-radius: 4px 10px 10px 4px;
  background: var(--yellow-tint);
  font-size: 0.88rem;
  line-height: 1.55;
  color: #4a4210;
}
.note strong {
  display: block;
  margin-bottom: 2px;
  color: var(--blue);
}

/* Small phones */
@media (max-width: 359px) {
  .page {
    padding: 8px;
  }
  .panel {
    padding: 22px 16px;
  }
  .btn {
    font-size: 1rem;
  }
}

/* Large phones / small tablets: more breathing room */
@media (min-width: 480px) {
  .page {
    padding: 24px;
  }
  .panel {
    padding: 36px 32px;
  }
}

/* Landscape phones: avoid a tall, cramped brand panel */
@media (max-height: 500px) and (orientation: landscape) {
  .page {
    align-items: flex-start;
  }
  .panel-brand {
    gap: 20px;
  }
}

/* Tablet and desktop: side by side */
@media (min-width: 820px) {
  .page {
    padding: 40px;
  }
  .shell {
    max-width: 980px;
    grid-template-columns: minmax(0, 1fr) minmax(0, 1.05fr);
    border-radius: 24px;
  }
  .panel {
    padding: 52px 44px;
  }
  .panel-brand {
    min-height: 580px;
  }
}

/* Wide desktop */
@media (min-width: 1200px) {
  .shell {
    max-width: 1060px;
  }
  .panel {
    padding: 60px 52px;
  }
}

@media (prefers-reduced-motion: reduce) {
  .btn {
    transition: none;
  }
}
</style>