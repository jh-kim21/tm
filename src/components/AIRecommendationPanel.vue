<script setup>
const confidence = 91.8
const circumference = 2 * Math.PI * 38
const dashArray = `${(confidence / 100) * circumference} ${circumference}`

const info = [
  { label: 'Device',       value: 'D30V-A' },
  { label: 'WFPROCESS',    value: '20nm KRF' },
  { label: 'MASKPROCESS',  value: 'Dry Etch' },
  { label: 'LAYERID',      value: 'GT-001' },
  { label: 'LAYER NAME',   value: 'GATE' },
  { label: 'MASKTYPE',     value: '6025 QZ' },
]

const adcCases = [
  { lot: 'LT220501', code: '2A', result: 'Pass' },
  { lot: 'LT220438', code: '2A', result: 'Pass' },
  { lot: 'LT220312', code: '2B', result: 'Fail' },
]
</script>

<template>
  <div class="panel">
    <div class="panel-header">
      <span class="badge-num">②</span>
      <span class="panel-title">추천 판정 <span class="sub">(AI Recommendation)</span></span>
    </div>

    <div class="body">
      <!-- AI code + gauge -->
      <div class="top-row">
        <div class="code-block">
          <div class="code-badge">2A</div>
          <div class="code-label">
            <span class="ai-tag">AI Recommendation</span>
            <span class="code-desc">Gate Layer Particle</span>
          </div>
        </div>

        <div class="gauge-block">
          <svg class="gauge-svg" viewBox="0 0 90 90">
            <circle cx="45" cy="45" r="38" fill="none" stroke="#e8edf4" stroke-width="9"/>
            <circle cx="45" cy="45" r="38" fill="none" stroke="#ff9800" stroke-width="9"
              :stroke-dasharray="dashArray"
              stroke-dashoffset="0"
              stroke-linecap="round"
              transform="rotate(-90 45 45)"/>
            <text x="45" y="41" text-anchor="middle" font-size="16" font-weight="700" fill="#1a2a4a">{{ confidence }}</text>
            <text x="45" y="53" text-anchor="middle" font-size="8" fill="#607090">Confidence</text>
          </svg>
          <div class="score-block">
            <div class="score-val">91.8</div>
            <div class="score-lbl">Score</div>
          </div>
        </div>
      </div>

      <!-- Info table -->
      <table class="info-table">
        <tbody>
          <tr v-for="r in info" :key="r.label">
            <td class="lbl">{{ r.label }}</td>
            <td class="val">{{ r.value }}</td>
          </tr>
        </tbody>
      </table>

      <!-- ADC similar cases -->
      <div class="adc-section">
        <div class="section-sub">
          <span class="dot-blue"></span>
          유사 ADC <b>{{ adcCases.length }}건</b>
        </div>
        <table class="adc-table">
          <thead>
            <tr>
              <th>LOT</th><th>판정코드</th><th>결과</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="c in adcCases" :key="c.lot">
              <td>{{ c.lot }}</td>
              <td><span class="code-chip">{{ c.code }}</span></td>
              <td><span :class="['result-chip', c.result === 'Pass' ? 'pass' : 'fail']">{{ c.result }}</span></td>
            </tr>
          </tbody>
        </table>
      </div>

      <!-- Grade -->
      <div class="grade-row">
        <span class="grade-lbl">결함등급 조건 항목</span>
        <span class="grade-badge">3</span>
        <span class="grade-desc">ADC 처리 대상</span>
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

.body { padding: 10px 12px; display: flex; flex-direction: column; gap: 10px; flex: 1; overflow: auto; }

.top-row {
  display: flex;
  gap: 12px;
  align-items: center;
}

.code-block {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 6px;
}
.code-badge {
  width: 64px; height: 64px;
  background: linear-gradient(135deg, #1565c0, #0288d1);
  color: white;
  border-radius: 12px;
  display: flex; align-items: center; justify-content: center;
  font-size: 26px; font-weight: 800;
  box-shadow: 0 3px 10px rgba(21,101,192,0.35);
  letter-spacing: -1px;
}
.ai-tag {
  display: block;
  font-size: 10px;
  color: #0288d1;
  font-weight: 700;
  background: #e3f2fd;
  padding: 2px 6px;
  border-radius: 3px;
}
.code-desc { font-size: 10px; color: #607090; }

.gauge-block {
  display: flex;
  align-items: center;
  gap: 8px;
  flex: 1;
  justify-content: flex-end;
}
.gauge-svg { width: 80px; height: 80px; }

.score-block { text-align: center; }
.score-val {
  font-size: 26px; font-weight: 800;
  color: #ff9800;
  line-height: 1;
}
.score-lbl { font-size: 10px; color: #607090; }

.info-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 11px;
}
.info-table tr { border-bottom: 1px solid #f0f4fa; }
.info-table tr:last-child { border-bottom: none; }
.info-table .lbl {
  width: 90px;
  color: #607090;
  padding: 4px 6px 4px 0;
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.3px;
}
.info-table .val {
  color: #1a2a4a;
  font-weight: 600;
  padding: 4px 0;
}

.adc-section {}
.section-sub {
  font-size: 11px;
  font-weight: 600;
  color: #1a2a4a;
  display: flex;
  align-items: center;
  gap: 5px;
  margin-bottom: 5px;
}
.dot-blue {
  width: 7px; height: 7px;
  background: #1565c0;
  border-radius: 50%;
}
.section-sub b { color: #1565c0; }

.adc-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 11px;
}
.adc-table th {
  background: #f0f4fa;
  color: #607090;
  font-weight: 600;
  padding: 4px 8px;
  text-align: left;
  font-size: 10px;
}
.adc-table td { padding: 4px 8px; border-bottom: 1px solid #f0f4fa; }

.code-chip {
  background: #e3f2fd;
  color: #1565c0;
  font-weight: 700;
  font-size: 11px;
  padding: 1px 6px;
  border-radius: 3px;
}
.result-chip {
  font-size: 10px;
  font-weight: 600;
  padding: 2px 6px;
  border-radius: 3px;
}
.result-chip.pass { background: #e8f5e9; color: #2e7d32; }
.result-chip.fail { background: #ffebee; color: #c62828; }

.grade-row {
  display: flex;
  align-items: center;
  gap: 8px;
  background: #fff8e1;
  border: 1px solid #ffe082;
  border-radius: 6px;
  padding: 7px 10px;
}
.grade-lbl { font-size: 11px; color: #795548; font-weight: 600; flex: 1; }
.grade-badge {
  width: 26px; height: 26px;
  background: #ff9800;
  color: white;
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 14px; font-weight: 800;
}
.grade-desc { font-size: 11px; color: #795548; }
</style>
