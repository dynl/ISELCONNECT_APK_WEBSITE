<script setup>
// No external components needed for this simple landing page
</script>

<template>
  <main class="landing-container">
    <div class="content-card">
      
      <!-- Hero Section -->
      <header class="text-center">
        <div class="logo-placeholder">⚡</div>
        <h1 class="app-title">ISELCONNECT</h1>
        <p class="app-subtitle">
          The official portal for residents and linemen. Report issues, check account status, and stay connected.
        </p>
      </header>

      <!-- Action Section -->
      <div class="action-section">
        <!-- 
          The href points to the file in your public folder. 
          The 'download' attribute forces the browser to download it.
        -->
        <a href="/iselconnect.apk" download="ISELCONNECT.apk" class="download-button">
          Download App (.apk)
        </a>
        <p class="version-text">Version 1.0 | Android Only</p>
      </div>

      <hr class="divider" />

      <!-- Installation Instructions -->
      <section class="instructions">
        <h2>How to Install on Android</h2>
        <ol>
          <li><strong>Download</strong> the file by clicking the blue button above.</li>
          <li><strong>Open</strong> the downloaded <code>.apk</code> file from your phone's notification panel or Downloads folder.</li>
          <li><strong>Allow Unknown Sources:</strong> If a security warning appears, tap "Settings" and toggle on <em>"Allow from this source"</em> to permit the installation.</li>
          <li><strong>Install</strong> the application and open it to log in.</li>
        </ol>
      </section>
      
    </div>
  </main>
</template>

<style scoped>
/* Base Layout */
.landing-container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f8fafc;
  padding: 20px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
}

.content-card {
  background: white;
  max-width: 500px;
  width: 100%;
  border-radius: 12px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  padding: 40px 30px;
}

/* Typography & Alignment */
.text-center {
  text-align: center;
}

.logo-placeholder {
  font-size: 48px;
  margin-bottom: 16px;
}

.app-title {
  color: #0f172a;
  font-size: 28px;
  font-weight: 800;
  margin: 0 0 8px 0;
}

.app-subtitle {
  color: #64748b;
  font-size: 16px;
  line-height: 1.5;
  margin: 0;
}

/* Download Button */
.action-section {
  margin: 32px 0;
  text-align: center;
}

.download-button {
  display: inline-block;
  width: 100%;
  background-color: #2563eb;
  color: white;
  font-size: 18px;
  font-weight: bold;
  text-decoration: none;
  padding: 16px 24px;
  border-radius: 8px;
  transition: background-color 0.2s ease;
  box-sizing: border-box;
}

.download-button:hover {
  background-color: #1d4ed8;
}

.version-text {
  font-size: 13px;
  color: #94a3b8;
  margin-top: 12px;
}

.divider {
  border: 0;
  height: 1px;
  background: #e2e8f0;
  margin: 32px 0;
}

/* Instructions */
.instructions h2 {
  font-size: 18px;
  color: #334155;
  margin-top: 0;
  margin-bottom: 16px;
}

.instructions ol {
  padding-left: 20px;
  margin: 0;
  color: #475569;
}

.instructions li {
  margin-bottom: 12px;
  line-height: 1.5;
}

.instructions li:last-child {
  margin-bottom: 0;
}
</style>