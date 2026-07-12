<script setup>
const totalScore = 91.8

const criteria = [
  { label: 'Image Similarity',    value: 43.2, color: '#1565c0' },
  { label: 'Layer Match',         value: 18.0, color: '#1565c0' },
  { label: 'Device Match',        value: 9.5,  color: '#1565c0' },
  { label: 'Mask Process Match',  value: 8.7,  color: '#1565c0' },
  { label: 'Recent Final History',value: 7.4,  color: '#1565c0' },
  { label: 'SOP Rule Match',      value: 8.0,  color: '#1565c0' },
  { label: 'Exception / Conflict',value: -3.0, color: '#e53935' },
]

const axisMin = -20
const axisMax = 50
const axisRange = axisMax - axisMin
const zeroPct = ((0 - axisMin) / axisRange) * 100

function barStyle(value) {
  const startPct = value >= 0 ? zeroPct : ((value - axisMin) / axisRange) * 100
  const widthPct = (Math.abs(value) / axisRange) * 100
  return { left: startPct + '%', width: widthPct + '%' }
}

const axisTicks = [-20, -10, 0, 10, 20, 30, 40, 50]
</script>

<template>
  <div class="panel">
    <div class="panel-header">
      <span class="badge-num">③</span>
      <span class="panel-title">추천 점수 구성 <span class="sub">(Score Breakdown)</span></span>
    </div>
    <div class="body">
      <div class="total-row">
        <span class="total-label">Total Score</span>
        <span class="total-val">{{ totalScore }}<span class="total-max"> / 100</span></span>
      </div>

      <div class="criteria-list">
        <div v-for="c in criteria" :key="c.label" class="criterion-row">
          <span class="crit-label">{{ c.label }}</span>
          <div class="bar-track">
            <div class="zero-line" :style="{ left: zeroPct + '%' }"/>
            <div class="bar-fill" :style="{ ...barStyle(c.value), background: c.color }"/>
          </div>
          <span class="crit-value" :style="{ color: c.color }">{{ c.value.toFixed(1) }}</span>
        </div>
      </div>

      <div class="axis-row">
        <span v-for="t in axisTicks" :key="t">{{ t }}</span>
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
  flex-shrink: 0;
}
.badge-num {
  display: inline-flex; align-items: center; justify-content: center;
  width: 20px; height: 20px;
  background: #1565c0; color: white;
  border-radius: 50%; font-size: 11px; font-weight: 700;
}
.panel-title { font-size: 12px; font-weight: 700; color: #1a2a4a; }
.panel-title .sub { font-weight: 400; color: #607090; font-size: 11px; }

.body { padding: 12px; display: flex; flex-direction: column; gap: 10px; flex: 1; overflow: auto; min-height: 0; }

.total-row {
  display: flex;
  align-items: baseline;
  justify-content: space-between;
}
.total-label { font-size: 12px; color: #607090; font-weight: 600; }
.total-val { font-size: 28px; font-weight: 800; color: #1565c0; }
.total-max { font-size: 13px; font-weight: 400; color: #90a0b8; }

.criteria-list { display: flex; flex-direction: column; gap: 10px; }

.criterion-row {
  display: grid;
  grid-template-columns: 120px 1fr 38px;
  align-items: center;
  gap: 8px;
}
.crit-label { font-size: 11px; color: #2c3345; }
.crit-value { font-size: 11px; font-weight: 700; text-align: right; }

.bar-track {
  position: relative;
  height: 10px;
  background: #f0f4fa;
  border-radius: 2px;
}
.zero-line {
  position: absolute;
  top: -2px;
  bottom: -2px;
  width: 1px;
  background: #c0c8d8;
}
.bar-fill {
  position: absolute;
  top: 0;
  height: 100%;
  border-radius: 2px;
}

.axis-row {
  display: flex;
  justify-content: space-between;
  font-size: 9px;
  color: #90a0b8;
  padding-left: 120px;
  border-top: 1px solid #eef1f7;
  padding-top: 6px;
}

@media print {
  .panel-header { padding: 4px 8px 3px; }
  .badge-num { width: 14px; height: 14px; font-size: 9px; }
  .panel-title { font-size: 10px; }
  .body { padding: 6px 8px; gap: 6px; }
  .total-val { font-size: 18px; }
  .criteria-list { gap: 4px; }
  .bar-track { height: 7px; }
  .axis-row { padding-top: 3px; }
}
</style>
