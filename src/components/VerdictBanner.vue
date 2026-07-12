<script setup>
const code = '2A'
const confidence = 91.8
const evidenceLevel = 'Strong'
</script>

<template>
  <div class="verdict-banner">
    <div class="verdict-item verdict-code">
      <span class="verdict-label">추천 코드</span>
      <span class="verdict-code-val">{{ code }}</span>
    </div>
    <div class="verdict-divider"/>
    <div class="verdict-item">
      <span class="verdict-label">신뢰도</span>
      <span class="verdict-conf-val">{{ confidence }}%</span>
    </div>
    <div class="verdict-divider"/>
    <div class="verdict-item">
      <span class="verdict-label">Evidence Level</span>
      <span class="verdict-evidence-val">
        <svg viewBox="0 0 20 22" class="shield-icon">
          <path d="M10 1 L18 4 V10 C18 15 14.5 19 10 21 C5.5 19 2 15 2 10 V4 Z" fill="#ffffff"/>
          <path d="M6 10.5 L9 13.5 L14 7.5" fill="none" stroke="#2e7d32" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
        {{ evidenceLevel }}
      </span>
    </div>
  </div>
</template>

<style scoped>
.verdict-banner {
  display: flex;
  align-items: center;
  gap: 20px;
  padding: 12px 20px;
  background: linear-gradient(135deg, #1b5e20, #2e7d32);
  box-shadow: 0 1px 6px rgba(0,0,0,0.15);
}

.verdict-item {
  display: flex;
  align-items: center;
  gap: 10px;
}
.verdict-label {
  font-size: 11px;
  font-weight: 600;
  color: rgba(255,255,255,0.75);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.verdict-code-val {
  font-size: 26px;
  font-weight: 800;
  color: white;
  line-height: 1;
}
.verdict-conf-val {
  font-size: 22px;
  font-weight: 800;
  color: white;
  line-height: 1;
}
.verdict-evidence-val {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 16px;
  font-weight: 700;
  color: white;
}
.shield-icon { width: 15px; height: 17px; flex-shrink: 0; }

.verdict-divider {
  width: 1px;
  height: 26px;
  background: rgba(255,255,255,0.25);
}

@media print {
  .verdict-banner { padding: 6px 12px; gap: 12px; }
  .verdict-code-val { font-size: 18px; }
  .verdict-conf-val { font-size: 15px; }
  .verdict-evidence-val { font-size: 12px; }
  .verdict-divider { height: 18px; }
}
</style>
