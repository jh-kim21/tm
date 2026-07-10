<script setup>
const reasons = [
  '유사사례 50건 중 44건 (88%)이 2A로 최종 판정됨',
  '동일 Layer / 동일 Mask Process 사례 39건 중 39건이 2A',
  '최근 SOP Rule (2026-07-01 적용)과 일치',
]

const cautions = [
  'ADC는 2B를 62%로 제안함',
  'Critical Area 근처 여부 확인 필요',
]
</script>

<template>
  <div class="panel">
    <div class="panel-header">
      <span class="badge-num">②</span>
      <span class="panel-title">추천 판정 <span class="sub">(AI Recommendation)</span></span>
    </div>

    <div class="body">
      <div class="summary-row">
        <div class="summary-block">
          <div class="summary-label">Recommended Code</div>
          <div class="summary-code">2A</div>
        </div>
        <div class="summary-block">
          <div class="summary-label">Confidence</div>
          <div class="summary-conf">91.8%</div>
        </div>
        <div class="summary-block">
          <div class="summary-label">Evidence Level</div>
          <div class="summary-evidence">
            <svg viewBox="0 0 20 22" class="shield-icon">
              <path d="M10 1 L18 4 V10 C18 15 14.5 19 10 21 C5.5 19 2 15 2 10 V4 Z" fill="#1565c0"/>
              <path d="M6 10.5 L9 13.5 L14 7.5" fill="none" stroke="white" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
            <span>Strong</span>
          </div>
        </div>
      </div>

      <div class="why-section">
        <div class="why-title">왜 2A인가? (요약)</div>
        <ol class="why-list">
          <li v-for="(r, i) in reasons" :key="i">{{ r }}</li>
        </ol>
      </div>

      <div class="caution-box">
        <div class="caution-title">주의 조건</div>
        <ul class="caution-list">
          <li v-for="(c, i) in cautions" :key="i">{{ c }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
.panel {
  background: white;
  border-radius: 8px;
  box-shadow: 0 1px 6px rgba(0,0,0,0.1);
  display: flex;
  flex-direction: column;
  overflow: hidden;
  height: 100%;
}

.panel-header {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 12px 6px;
  border-bottom: 1px solid #eef1f7;
  background: #f8fafd;
}
.badge-num {
  display: inline-flex; align-items: center; justify-content: center;
  width: 20px; height: 20px;
  background: #1565c0; color: white;
  border-radius: 50%; font-size: 11px; font-weight: 700;
}
.panel-title { font-size: 12px; font-weight: 700; color: #1a2a4a; }
.panel-title .sub { font-weight: 400; color: #607090; font-size: 11px; }

.body { padding: 12px; display: flex; flex-direction: column; gap: 14px; flex: 1; overflow: auto; }

.summary-row {
  display: flex;
  justify-content: space-between;
  gap: 10px;
}
.summary-block { display: flex; flex-direction: column; gap: 4px; align-items: flex-start; }
.summary-label { font-size: 10px; color: #90a0b8; }
.summary-code { font-size: 26px; font-weight: 800; color: #2e7d32; }
.summary-conf { font-size: 22px; font-weight: 800; color: #1a2a4a; }
.summary-evidence {
  display: flex;
  align-items: center;
  gap: 5px;
  font-size: 14px;
  font-weight: 700;
  color: #1a2a4a;
}
.shield-icon { width: 16px; height: 18px; flex-shrink: 0; }

.why-section {}
.why-title {
  font-size: 12px;
  font-weight: 700;
  color: #1a2a4a;
  margin-bottom: 6px;
}
.why-list {
  margin: 0;
  padding-left: 18px;
  display: flex;
  flex-direction: column;
  gap: 4px;
  font-size: 11px;
  color: #2c3345;
}

.caution-box {
  background: #fff8e1;
  border: 1px solid #ffe082;
  border-radius: 6px;
  padding: 8px 10px;
}
.caution-title {
  font-size: 11px;
  font-weight: 700;
  color: #795548;
  margin-bottom: 4px;
}
.caution-list {
  margin: 0;
  padding-left: 16px;
  display: flex;
  flex-direction: column;
  gap: 3px;
  font-size: 11px;
  color: #795548;
}
</style>
