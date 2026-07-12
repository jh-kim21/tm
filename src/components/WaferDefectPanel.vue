<script setup>
import mainDefectImg from '../assets/defect-images/main-defect.png'
import gallery1 from '../assets/defect-images/gallery-1.png'
import gallery2 from '../assets/defect-images/gallery-2.png'
import gallery3 from '../assets/defect-images/gallery-3.png'
import gallery4 from '../assets/defect-images/gallery-4.png'
import gallery5 from '../assets/defect-images/gallery-5.png'
import gallery6 from '../assets/defect-images/gallery-6.png'

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
  { id: 1, label: 'DEF-042', active: true,  img: gallery1 },
  { id: 2, label: 'DEF-041', active: false, img: gallery2 },
  { id: 3, label: 'REF-2A',  active: false, img: gallery3 },
  { id: 4, label: 'REF-2B',  active: false, img: gallery4 },
  { id: 5, label: 'REF-2A',  active: false, img: gallery5 },
  { id: 6, label: 'REF-1A',  active: false, img: gallery6 },
]

const metaInfo = [
  { label: 'Location',            value: '(X: 12.53, Y: 8.72)' },
  { label: 'Defect Size',         value: '0.38um' },
  { label: 'Defect Class (ADC)',  value: '2B (62.1%)' },
  { label: 'Review Code',         value: '-' },
  { label: 'Final Code (History)',value: '-' },
  { label: 'Reporter',            value: 'Engineer Lee' },
  { label: 'Review Time',         value: '2026-07-15 10:21:33' },
]
</script>

<template>
  <div class="panel">
    <div class="panel-header">
      <span class="badge-num">①</span>
      <span class="panel-title">현재 Defect 정보</span>
    </div>

    <div class="body">
      <div class="top-row">
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
          <div class="legend-title">Defect</div>
          <div class="legend">
            <span><i style="background:#f44336"></i>&ge; 10</span>
            <span><i style="background:#ff9800"></i>5 ~ 9</span>
            <span><i style="background:#fdd835"></i>1 ~ 4</span>
            <span><i style="background:#9e9e9e"></i>0</span>
          </div>
          <div class="defect-stat">
            <div><span>Total Defect</span><b>128</b></div>
            <div><span>Selected</span><b>1</b></div>
          </div>
        </div>

        <!-- Defect Image + Meta -->
        <div class="image-section">
          <div class="sub-label">Defect Image</div>
          <div class="image-row">
            <div class="def-img-wrap">
              <img class="def-img" :src="mainDefectImg" alt="Defect image DEF-042"/>
              <svg class="def-img-overlay" viewBox="0 0 220 160" preserveAspectRatio="none">
                <!-- Defect area highlight -->
                <rect x="98" y="76" width="24" height="20" fill="none" stroke="#f44336" stroke-width="1.3" stroke-dasharray="3,2" opacity="0.9"/>
                <line x1="88" y1="86" x2="132" y2="86" stroke="#f44336" stroke-width="0.6" opacity="0.6"/>
                <line x1="110" y1="70" x2="110" y2="102" stroke="#f44336" stroke-width="0.6" opacity="0.6"/>
                <!-- Scale bar -->
                <line x1="180" y1="148" x2="210" y2="148" stroke="white" stroke-width="1.5"/>
                <text x="195" y="157" text-anchor="middle" fill="white" font-size="8">2 um</text>
                <!-- ADC marker -->
                <rect x="2" y="2" width="42" height="14" fill="#f44336" rx="2" opacity="0.85"/>
                <text x="23" y="12" text-anchor="middle" fill="white" font-size="9" font-weight="bold">DEF-042</text>
              </svg>
            </div>
            <div class="meta-list">
              <div class="meta-row" v-for="m in metaInfo" :key="m.label">
                <span class="meta-label">{{ m.label }}</span>
                <span class="meta-value">{{ m.value }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Image Gallery -->
      <div class="gallery-section">
        <div class="sub-label">Image Gallery</div>
        <div class="thumb-strip">
          <div v-for="t in thumbnails" :key="t.id" :class="['thumb', { active: t.active }]">
            <div class="thumb-img-wrap">
              <img :src="t.img" :alt="t.label"/>
              <svg v-if="t.active" class="thumb-overlay" viewBox="0 0 60 44" preserveAspectRatio="none">
                <rect x="24" y="16" width="14" height="12" fill="none" stroke="#f44336" stroke-width="1" stroke-dasharray="2,1.5"/>
              </svg>
            </div>
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

.body {
  display: flex;
  flex-direction: column;
  gap: 8px;
  flex: 1;
  padding: 8px 10px;
  overflow: auto;
}

.top-row {
  display: flex;
  gap: 10px;
  align-items: flex-start;
}

.wafer-section {
  flex: 0 0 190px;
}

.image-section {
  flex: 1;
  min-width: 0;
}

.gallery-section {
  border-top: 1px solid #eef1f7;
  padding-top: 8px;
}

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
  max-height: 155px;
  display: block;
}

.image-row {
  display: flex;
  gap: 8px;
}

.meta-list {
  flex: 0 0 150px;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.meta-row {
  display: flex;
  flex-direction: column;
  gap: 0;
}

.meta-label {
  font-size: 9px;
  color: #90a0b8;
}

.meta-value {
  font-size: 11px;
  font-weight: 600;
  color: #1a2a4a;
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

.legend-title {
  font-size: 9px;
  font-weight: 700;
  color: #90a0b8;
  text-transform: uppercase;
  letter-spacing: 0.4px;
  margin-top: 4px;
}

.defect-stat {
  display: flex;
  flex-direction: column;
  gap: 2px;
  font-size: 10px;
  color: #607090;
  margin-top: 5px;
}
.defect-stat > div { display: flex; justify-content: space-between; gap: 8px; }
.defect-stat b { color: #1a2a4a; }

.def-img-wrap {
  position: relative;
  flex: 1;
  min-width: 0;
  border-radius: 6px;
  overflow: hidden;
  border: 1px solid #1a3a5a;
  line-height: 0;
}
.def-img { width: 100%; display: block; }
.def-img-overlay {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}

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
.thumb-img-wrap { position: relative; width: 100%; line-height: 0; }
.thumb-img-wrap img { width: 100%; border-radius: 3px; display: block; }
.thumb-overlay { position: absolute; inset: 0; width: 100%; height: 100%; }
.thumb span { font-size: 9px; color: #607090; }
.thumb.active span { color: #1565c0; font-weight: 600; }

@media print {
  .panel-header { padding: 4px 8px 3px; }
  .badge-num { width: 14px; height: 14px; font-size: 9px; }
  .panel-title { font-size: 10px; }
  .body { padding: 5px 8px; gap: 5px; }
  .wafer-section { flex: 0 0 130px; }
  .wafer-svg { max-height: 105px; }
  .meta-list { flex: 0 0 130px; gap: 2px; }
  .gallery-section { padding-top: 5px; }
  .thumb-strip { margin-top: 4px; }
}
</style>
