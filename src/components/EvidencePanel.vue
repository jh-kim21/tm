<script setup>
const shapeParams = [
  { label: 'Circularity',  val: 0.82, ref: 0.85 },
  { label: 'Area (μm²)',   val: 0.047, ref: 0.05 },
  { label: 'Aspect Ratio', val: 1.32, ref: 1.4 },
  { label: 'Roughness',    val: 0.14, ref: 0.12 },
]

const stats = [
  { month: 'Jan', count: 4 },
  { month: 'Feb', count: 7 },
  { month: 'Mar', count: 3 },
  { month: 'Apr', count: 9 },
  { month: 'May', count: 6 },
  { month: 'Jun', count: 11 },
  { month: 'Jul', count: 5 },
]
const maxCount = Math.max(...stats.map(s => s.count))

const sopRules = [
  { field: 'Layer',    value: 'GATE (GT-001)' },
  { field: 'Size',     value: '0.2 ~ 0.5 μm' },
  { field: 'Type',     value: 'Particle' },
  { field: 'Code',     value: '2A' },
  { field: 'Action',   value: 'ADC 처리' },
]
</script>

<template>
  <div class="panel">
    <div class="panel-header">
      <span class="badge-num">④</span>
      <span class="panel-title">근거 Evidence 제시</span>
    </div>

    <div class="body">
      <!-- Evidence 1: Image Similarity -->
      <div class="ev-card">
        <div class="ev-title">Evidence 1<span class="ev-sub">Image Similarity</span></div>
        <div class="ev-score-chip">98.1%</div>
        <div class="img-pair">
          <!-- Current defect -->
          <div class="img-box">
            <svg viewBox="0 0 80 60">
              <rect width="80" height="60" fill="#080c10"/>
              <rect x="0" y="14" width="80" height="7" fill="#0e2235"/>
              <rect x="0" y="35" width="80" height="7" fill="#0e2235"/>
              <line x1="0" y1="14" x2="80" y2="14" stroke="#3a8abb" stroke-width="0.8"/>
              <line x1="0" y1="21" x2="80" y2="21" stroke="#3a8abb" stroke-width="0.8"/>
              <line x1="0" y1="35" x2="80" y2="35" stroke="#3a8abb" stroke-width="0.8"/>
              <line x1="0" y1="42" x2="80" y2="42" stroke="#3a8abb" stroke-width="0.8"/>
              <circle cx="42" cy="28" r="7" fill="none" stroke="#f44336" stroke-width="1" stroke-dasharray="2,2"/>
              <ellipse cx="42" cy="28" rx="3" ry="2" fill="#c0392b" opacity="0.9"/>
            </svg>
            <span>현재 결함</span>
          </div>
          <div class="sim-arrow">→</div>
          <!-- Reference -->
          <div class="img-box">
            <svg viewBox="0 0 80 60">
              <rect width="80" height="60" fill="#080c10"/>
              <rect x="0" y="14" width="80" height="7" fill="#0e2235"/>
              <rect x="0" y="35" width="80" height="7" fill="#0e2235"/>
              <line x1="0" y1="14" x2="80" y2="14" stroke="#3a8abb" stroke-width="0.8"/>
              <line x1="0" y1="21" x2="80" y2="21" stroke="#3a8abb" stroke-width="0.8"/>
              <line x1="0" y1="35" x2="80" y2="35" stroke="#3a8abb" stroke-width="0.8"/>
              <line x1="0" y1="42" x2="80" y2="42" stroke="#3a8abb" stroke-width="0.8"/>
              <circle cx="40" cy="27" r="6" fill="none" stroke="#42a5f5" stroke-width="1"/>
              <ellipse cx="40" cy="27" rx="2.5" ry="1.8" fill="#1565c0" opacity="0.8"/>
            </svg>
            <span>참조 (2A)</span>
          </div>
        </div>
        <div class="sim-bar-row">
          <span>유사도</span>
          <div class="sim-bar"><div class="sim-fill" style="width:98.1%"></div></div>
          <b>98.1%</b>
        </div>
      </div>

      <!-- Evidence 2: Shape Analysis -->
      <div class="ev-card">
        <div class="ev-title">Evidence 2<span class="ev-sub">형태 분석</span></div>
        <table class="shape-table">
          <thead>
            <tr><th>파라미터</th><th>측정값</th><th>기준값</th><th>상태</th></tr>
          </thead>
          <tbody>
            <tr v-for="p in shapeParams" :key="p.label">
              <td>{{ p.label }}</td>
              <td><b>{{ p.val }}</b></td>
              <td class="ref">{{ p.ref }}</td>
              <td>
                <span :class="['status-dot', Math.abs(p.val - p.ref) / p.ref < 0.1 ? 'ok' : 'warn']">
                  {{ Math.abs(p.val - p.ref) / p.ref < 0.1 ? '✓' : '△' }}
                </span>
              </td>
            </tr>
          </tbody>
        </table>
        <div class="shape-match-score">형태 일치도 <b>87.5%</b></div>
      </div>

      <!-- Evidence 3: SOP Rule -->
      <div class="ev-card">
        <div class="ev-title">Evidence 3<span class="ev-sub">SOP Rule</span></div>
        <div class="sop-rule-id">GT-2A-001</div>
        <table class="shape-table">
          <tbody>
            <tr v-for="r in sopRules" :key="r.field">
              <td class="ref">{{ r.field }}</td>
              <td><b>{{ r.value }}</b></td>
            </tr>
          </tbody>
        </table>
        <div class="sop-comply">
          <span class="comply-badge">SOP 준수 96%</span>
        </div>
      </div>

      <!-- Evidence 4: Shape Distribution -->
      <div class="ev-card">
        <div class="ev-title">Evidence 4<span class="ev-sub">형태 분석 표현</span></div>
        <div class="radar-wrap">
          <svg viewBox="0 0 110 110" class="radar-svg">
            <!-- Background rings -->
            <polygon points="55,15 88,36 88,74 55,95 22,74 22,36" fill="none" stroke="#e0e8f0" stroke-width="1"/>
            <polygon points="55,27 79,42 79,68 55,83 31,68 31,42" fill="none" stroke="#e0e8f0" stroke-width="1"/>
            <polygon points="55,39 70,48 70,62 55,71 40,62 40,48" fill="none" stroke="#e0e8f0" stroke-width="1"/>
            <!-- Axes -->
            <line x1="55" y1="15" x2="55" y2="55" stroke="#d0d8e4" stroke-width="0.7"/>
            <line x1="88" y1="36" x2="55" y2="55" stroke="#d0d8e4" stroke-width="0.7"/>
            <line x1="88" y1="74" x2="55" y2="55" stroke="#d0d8e4" stroke-width="0.7"/>
            <line x1="55" y1="95" x2="55" y2="55" stroke="#d0d8e4" stroke-width="0.7"/>
            <line x1="22" y1="74" x2="55" y2="55" stroke="#d0d8e4" stroke-width="0.7"/>
            <line x1="22" y1="36" x2="55" y2="55" stroke="#d0d8e4" stroke-width="0.7"/>
            <!-- Data polygon (current) -->
            <polygon points="55,22 82,39 83,68 55,88 29,68 28,40"
              fill="rgba(21,101,192,0.2)" stroke="#1565c0" stroke-width="1.5"/>
            <!-- Reference polygon -->
            <polygon points="55,24 80,40 80,67 55,86 30,67 30,41"
              fill="none" stroke="#ff9800" stroke-width="1" stroke-dasharray="3,2"/>
            <!-- Labels -->
            <text x="55" y="12" text-anchor="middle" font-size="7" fill="#607090">Circ</text>
            <text x="94" y="38" font-size="7" fill="#607090">Area</text>
            <text x="90" y="77" font-size="7" fill="#607090">AR</text>
            <text x="44" y="102" font-size="7" fill="#607090">Rough</text>
            <text x="8" y="77" font-size="7" fill="#607090">Len</text>
            <text x="6" y="38" font-size="7" fill="#607090">Wid</text>
          </svg>
        </div>
        <div class="legend-small">
          <span><i style="background:#1565c0"></i>측정값</span>
          <span><i style="background:#ff9800; opacity:0.7"></i>기준</span>
        </div>
      </div>

      <!-- Evidence 5: Statistics -->
      <div class="ev-card">
        <div class="ev-title">Evidence 5<span class="ev-sub">발생/처리 통계</span></div>
        <div class="stat-chart">
          <div v-for="s in stats" :key="s.month" class="stat-col">
            <div class="bar-wrap">
              <div class="stat-bar"
                :style="{ height: (s.count / maxCount * 70) + 'px', background: '#1565c0' }"/>
            </div>
            <span class="stat-month">{{ s.month }}</span>
            <span class="stat-cnt">{{ s.count }}</span>
          </div>
        </div>
        <div class="stat-footer">
          총 45건 발생 | 2A 판정 <b>38건 (84.4%)</b>
        </div>
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
}

.panel-header {
  display: flex; align-items: center; gap: 8px;
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

.body {
  display: flex;
  gap: 8px;
  padding: 8px;
  overflow-x: auto;
}

.ev-card {
  flex: 1;
  min-width: 160px;
  background: #f8fafd;
  border: 1px solid #e4e9f4;
  border-radius: 6px;
  padding: 8px;
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.ev-title {
  font-size: 10px;
  font-weight: 700;
  color: #1565c0;
  display: flex;
  flex-direction: column;
  gap: 1px;
}
.ev-sub { font-weight: 600; color: #2c3345; font-size: 11px; }

.ev-score-chip {
  display: inline-block;
  background: #e3f2fd;
  color: #1565c0;
  font-size: 12px;
  font-weight: 700;
  padding: 2px 8px;
  border-radius: 4px;
}

.img-pair {
  display: flex;
  align-items: center;
  gap: 4px;
}
.img-box {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2px;
}
.img-box svg { width: 100%; border-radius: 4px; border: 1px solid #1a3a5a; }
.img-box span { font-size: 9px; color: #607090; }
.sim-arrow { color: #90a0b8; font-size: 14px; }

.sim-bar-row {
  display: flex;
  align-items: center;
  gap: 5px;
  font-size: 10px;
  color: #607090;
}
.sim-bar { flex: 1; height: 5px; background: #e0e8f4; border-radius: 3px; overflow: hidden; }
.sim-fill { height: 100%; background: #1565c0; border-radius: 3px; }
.sim-bar-row b { color: #1565c0; font-size: 11px; }

.shape-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 10px;
}
.shape-table th {
  background: #eef1f7;
  color: #607090;
  font-weight: 600;
  padding: 3px 4px;
  text-align: left;
  font-size: 9px;
}
.shape-table td { padding: 3px 4px; border-bottom: 1px solid #eef1f7; color: #2c3345; }
.shape-table .ref { color: #90a0b8; }

.status-dot {
  display: inline-flex;
  align-items: center; justify-content: center;
  width: 16px; height: 16px;
  border-radius: 50%;
  font-size: 9px;
  font-weight: 700;
}
.status-dot.ok  { background: #e8f5e9; color: #2e7d32; }
.status-dot.warn { background: #fff8e1; color: #f57f17; }

.shape-match-score {
  font-size: 10px;
  color: #607090;
  text-align: right;
}
.shape-match-score b { color: #1565c0; }

.sop-rule-id {
  display: inline-block;
  background: #e8eaf6;
  color: #3949ab;
  font-size: 11px;
  font-weight: 700;
  padding: 2px 8px;
  border-radius: 4px;
}

.sop-comply { text-align: center; margin-top: 2px; }
.comply-badge {
  background: #e8f5e9;
  color: #2e7d32;
  font-size: 11px;
  font-weight: 700;
  padding: 3px 10px;
  border-radius: 12px;
}

.radar-wrap { display: flex; justify-content: center; }
.radar-svg { width: 110px; height: 110px; }

.legend-small {
  display: flex;
  gap: 8px;
  justify-content: center;
  font-size: 9px;
  color: #607090;
}
.legend-small i {
  display: inline-block;
  width: 10px; height: 3px;
  margin-right: 3px;
  vertical-align: middle;
  border-radius: 1px;
}

.stat-chart {
  display: flex;
  align-items: flex-end;
  gap: 4px;
  padding: 4px 0;
}
.stat-col {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2px;
}
.bar-wrap { height: 70px; display: flex; align-items: flex-end; }
.stat-bar {
  width: 14px;
  border-radius: 2px 2px 0 0;
  transition: height 0.4s ease;
  min-height: 3px;
}
.stat-month { font-size: 8px; color: #90a0b8; }
.stat-cnt { font-size: 9px; font-weight: 700; color: #1565c0; }

.stat-footer {
  font-size: 10px;
  color: #607090;
  text-align: center;
  border-top: 1px solid #e4e9f4;
  padding-top: 5px;
}
.stat-footer b { color: #1565c0; }
</style>
