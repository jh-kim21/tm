<script setup>
// Defect dots inside a circle (center 100,100 radius 82)
const defects = [
  { cx: 115, cy: 82,  type: 'current',  code: '2A' },
  { cx: 94,  cy: 62,  type: 'major',    code: '2B' },
  { cx: 132, cy: 108, type: 'major',    code: '3A' },
  { cx: 76,  cy: 118, type: 'minor',    code: '1A' },
  { cx: 82,  cy: 72,  type: 'minor',    code: '1B' },
  { cx: 142, cy: 88,  type: 'minor',    code: '1A' },
  { cx: 62,  cy: 102, type: 'minor',    code: '1A' },
  { cx: 124, cy: 140, type: 'minor',    code: '2A' },
  { cx: 88,  cy: 148, type: 'minor',    code: '1A' },
  { cx: 152, cy: 106, type: 'minor',    code: '1B' },
  { cx: 68,  cy: 84,  type: 'minor',    code: '1A' },
  { cx: 108, cy: 156, type: 'minor',    code: '1A' },
  { cx: 144, cy: 132, type: 'minor',    code: '2B' },
  { cx: 72,  cy: 138, type: 'minor',    code: '1A' },
  { cx: 92,  cy: 52,  type: 'minor',    code: '1A' },
  { cx: 160, cy: 100, type: 'minor',    code: '1A' },
  { cx: 48,  cy: 104, type: 'minor',    code: '1B' },
  { cx: 112, cy: 44,  type: 'minor',    code: '1A' },
]

const colorMap = {
  current: '#f44336',
  major:   '#ff9800',
  minor:   '#42a5f5',
}

const thumbnails = [
  { id: 1, label: 'DEF-042', active: true },
  { id: 2, label: 'DEF-041', active: false },
  { id: 3, label: 'REF-2A',  active: false },
  { id: 4, label: 'REF-2B',  active: false },
]
</script>

<template>
  <div class="panel">
    <div class="panel-header">
      <span class="badge-num">①</span>
      <span class="panel-title">WFR Defect 분석</span>
    </div>

    <div class="lot-bar">
      <span>LOT: <b>22050615-001</b></span>
      <span>B132MM</span>
      <span>STORM</span>
      <span>M/S: M(A)</span>
      <span>FLMap: <b>5</b></span>
    </div>

    <div class="body">
      <!-- Wafer Map -->
      <div class="wafer-section">
        <div class="sub-label">Wafer Map</div>
        <svg class="wafer-svg" viewBox="0 0 200 200">
          <!-- Grid lines -->
          <defs>
            <clipPath id="waferClip">
              <circle cx="100" cy="100" r="83"/>
            </clipPath>
          </defs>
          <g clip-path="url(#waferClip)" opacity="0.15">
            <line v-for="i in 10" :key="'h'+i" :x1="0" :y1="i*20" :x2="200" :y2="i*20" stroke="#607080" stroke-width="0.5"/>
            <line v-for="i in 10" :key="'v'+i" :x1="i*20" :y1="0" :x2="i*20" :y2="200" stroke="#607080" stroke-width="0.5"/>
          </g>
          <!-- Wafer boundary -->
          <circle cx="100" cy="100" r="83" fill="#1a2535" stroke="#3a5070" stroke-width="1.5"/>
          <!-- Notch at bottom -->
          <path d="M 94 183 Q 100 188 106 183" fill="none" stroke="#3a5070" stroke-width="2"/>
          <!-- Defect dots -->
          <g v-for="d in defects" :key="d.cx+','+d.cy">
            <circle v-if="d.type === 'current'"
              :cx="d.cx" :cy="d.cy" r="7"
              fill="none" stroke="#f44336" stroke-width="1.5" stroke-dasharray="3,2" opacity="0.9"/>
            <circle :cx="d.cx" :cy="d.cy" :r="d.type === 'current' ? 4 : 3"
              :fill="colorMap[d.type]" opacity="0.9"/>
          </g>
          <!-- Crosshair on current defect -->
          <line x1="107" y1="82" x2="123" y2="82" stroke="#f44336" stroke-width="0.8" opacity="0.7"/>
          <line x1="115" y1="74" x2="115" y2="90" stroke="#f44336" stroke-width="0.8" opacity="0.7"/>
        </svg>
        <div class="legend">
          <span><i style="background:#f44336"></i>현재 결함</span>
          <span><i style="background:#ff9800"></i>Major</span>
          <span><i style="background:#42a5f5"></i>Minor</span>
        </div>
        <div class="defect-stat">총 결함: <b>18</b>개 | 현재: <b>DEF-042</b></div>
      </div>

      <!-- Defect Image -->
      <div class="image-section">
        <div class="sub-label">Defect Image</div>
        <div class="def-img-wrap">
          <svg class="def-img" viewBox="0 0 220 160">
            <!-- SEM-like image background -->
            <rect width="220" height="160" fill="#080c10"/>
            <!-- Circuit pattern lines -->
            <rect x="0"   y="30"  width="220" height="18" fill="#0e2235" opacity="0.9"/>
            <rect x="0"   y="72"  width="220" height="14" fill="#0e2235" opacity="0.9"/>
            <rect x="0"   y="112" width="220" height="18" fill="#0e2235" opacity="0.9"/>
            <!-- Vertical contacts -->
            <rect x="22"  y="25" width="14" height="110" fill="#122a40" opacity="0.8"/>
            <rect x="68"  y="25" width="10" height="110" fill="#122a40" opacity="0.8"/>
            <rect x="112" y="25" width="14" height="110" fill="#122a40" opacity="0.8"/>
            <rect x="158" y="25" width="10" height="110" fill="#122a40" opacity="0.8"/>
            <rect x="194" y="25" width="14" height="110" fill="#122a40" opacity="0.8"/>
            <!-- Bright edges (gates) -->
            <line x1="0" y1="30"  x2="220" y2="30"  stroke="#4a9acc" stroke-width="1.2"/>
            <line x1="0" y1="48"  x2="220" y2="48"  stroke="#4a9acc" stroke-width="1.2"/>
            <line x1="0" y1="72"  x2="220" y2="72"  stroke="#4a9acc" stroke-width="1"/>
            <line x1="0" y1="86"  x2="220" y2="86"  stroke="#4a9acc" stroke-width="1"/>
            <line x1="0" y1="112" x2="220" y2="112" stroke="#4a9acc" stroke-width="1.2"/>
            <line x1="0" y1="130" x2="220" y2="130" stroke="#4a9acc" stroke-width="1.2"/>
            <!-- Defect area highlight -->
            <circle cx="118" cy="76" r="18" fill="none" stroke="#f44336" stroke-width="1.5" stroke-dasharray="4,3" opacity="0.85"/>
            <!-- Defect particle -->
            <ellipse cx="118" cy="76" rx="6" ry="4" fill="#c0392b" opacity="0.9"/>
            <ellipse cx="121" cy="79" rx="3" ry="2" fill="#e74c3c" opacity="0.7"/>
            <!-- Scale bar -->
            <line x1="180" y1="148" x2="210" y2="148" stroke="white" stroke-width="1.5"/>
            <text x="195" y="157" text-anchor="middle" fill="white" font-size="8">0.5 μm</text>
            <!-- ADC marker -->
            <rect x="2" y="2" width="42" height="14" fill="#f44336" rx="2" opacity="0.85"/>
            <text x="23" y="12" text-anchor="middle" fill="white" font-size="9" font-weight="bold">DEF-042</text>
          </svg>
        </div>

        <!-- Thumbnail strip -->
        <div class="thumb-strip">
          <div v-for="t in thumbnails" :key="t.id" :class="['thumb', { active: t.active }]">
            <svg viewBox="0 0 60 44">
              <rect width="60" height="44" fill="#0a0f18"/>
              <rect x="0" y="10" width="60" height="6" fill="#0e2235"/>
              <rect x="0" y="26" width="60" height="6" fill="#0e2235"/>
              <line x1="0" y1="10" x2="60" y2="10" stroke="#2a6a9a" stroke-width="0.8"/>
              <line x1="0" y1="16" x2="60" y2="16" stroke="#2a6a9a" stroke-width="0.8"/>
              <line x1="0" y1="26" x2="60" y2="26" stroke="#2a6a9a" stroke-width="0.8"/>
              <line x1="0" y1="32" x2="60" y2="32" stroke="#2a6a9a" stroke-width="0.8"/>
              <circle v-if="t.active" cx="32" cy="20" r="5" fill="none" stroke="#f44336" stroke-width="1" stroke-dasharray="2,2"/>
              <circle v-if="t.active" cx="32" cy="20" r="2" fill="#f44336" opacity="0.8"/>
            </svg>
            <span>{{ t.label }}</span>
          </div>
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
  display: inline-flex;
  align-items: center; justify-content: center;
  width: 20px; height: 20px;
  background: #1565c0;
  color: white;
  border-radius: 50%;
  font-size: 11px; font-weight: 700;
}
.panel-title { font-size: 12px; font-weight: 700; color: #1a2a4a; }

.lot-bar {
  display: flex;
  gap: 10px;
  padding: 4px 12px;
  background: #f0f4fa;
  font-size: 10px;
  color: #4a5a72;
  border-bottom: 1px solid #e4e9f0;
  flex-wrap: wrap;
}
.lot-bar b { color: #1565c0; }

.body {
  display: flex;
  flex-direction: column;
  flex: 1;
  overflow: auto;
}

.wafer-section, .image-section {
  padding: 8px 10px;
}
.wafer-section { border-bottom: 1px solid #eef1f7; }

.sub-label {
  font-size: 10px;
  font-weight: 700;
  color: #607090;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-bottom: 4px;
}

.wafer-svg {
  width: 100%;
  max-height: 175px;
  display: block;
}

.legend {
  display: flex;
  gap: 10px;
  margin-top: 4px;
  font-size: 10px;
  color: #607090;
}
.legend i {
  display: inline-block;
  width: 8px; height: 8px;
  border-radius: 50%;
  margin-right: 3px;
  vertical-align: middle;
}

.defect-stat {
  font-size: 10px;
  color: #607090;
  margin-top: 3px;
}
.defect-stat b { color: #1565c0; }

.def-img-wrap {
  border-radius: 6px;
  overflow: hidden;
  border: 1px solid #1a3a5a;
}
.def-img { width: 100%; display: block; }

.thumb-strip {
  display: flex;
  gap: 6px;
  margin-top: 6px;
}
.thumb {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2px;
  cursor: pointer;
  border-radius: 4px;
  padding: 2px;
  border: 1.5px solid transparent;
  transition: border-color 0.15s;
}
.thumb:hover { border-color: #90b8e0; }
.thumb.active { border-color: #1565c0; }
.thumb svg { width: 100%; border-radius: 3px; }
.thumb span { font-size: 9px; color: #607090; }
.thumb.active span { color: #1565c0; font-weight: 600; }
</style>
