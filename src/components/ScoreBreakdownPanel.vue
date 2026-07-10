<script setup>
const totalScore = 91.8

const criteria = [
  { label: 'Image Similarity',  score: 95.2, color: '#1565c0', weight: '30%' },
  { label: 'Shape Match',       score: 87.5, color: '#0288d1', weight: '25%' },
  { label: 'Process Match',     score: 92.0, color: '#00838f', weight: '20%' },
  { label: 'Group Similarity',  score: 88.7, color: '#558b2f', weight: '15%' },
  { label: 'SOP Compliance',    score: 96.0, color: '#6a1b9a', weight: '7%'  },
  { label: 'Historical Match',  score: 84.3, color: '#4e342e', weight: '3%'  },
]
</script>

<template>
  <div class="panel">
    <div class="panel-header">
      <span class="badge-num">③</span>
      <span class="panel-title">수신 정수 비교 <span class="sub">(Score Breakdown)</span></span>
    </div>

    <div class="body">
      <div class="total-score">
        <div class="total-circle">
          <svg viewBox="0 0 80 80">
            <circle cx="40" cy="40" r="34" fill="none" stroke="#e8edf4" stroke-width="7"/>
            <circle cx="40" cy="40" r="34" fill="none" stroke="#1565c0" stroke-width="7"
              stroke-dasharray="213.6 213.6"
              stroke-linecap="round"
              transform="rotate(-90 40 40)"/>
            <text x="40" y="37" text-anchor="middle" font-size="14" font-weight="800" fill="#1a2a4a">{{ totalScore }}</text>
            <text x="40" y="48" text-anchor="middle" font-size="7" fill="#607090">TOTAL</text>
          </svg>
        </div>
        <div class="total-label">
          <div class="total-val">{{ totalScore }}<span>/100</span></div>
          <div class="total-lbl">종합 Score</div>
          <div class="total-grade grade-a">등급 A</div>
        </div>
      </div>

      <div class="criteria-list">
        <div v-for="c in criteria" :key="c.label" class="criterion-row">
          <div class="crit-top">
            <span class="crit-label">{{ c.label }}</span>
            <span class="crit-weight">가중 {{ c.weight }}</span>
            <span class="crit-score" :style="{ color: c.color }">{{ c.score }}</span>
          </div>
          <div class="bar-bg">
            <div class="bar-fill"
              :style="{ width: c.score + '%', background: c.color }"/>
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
.panel-title .sub { font-weight: 400; color: #607090; font-size: 11px; }

.body { padding: 12px; display: flex; flex-direction: column; gap: 14px; }

.total-score {
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 10px;
  background: linear-gradient(135deg, #e3f2fd, #e8eaf6);
  border-radius: 8px;
}
.total-circle svg { width: 72px; height: 72px; }

.total-val {
  font-size: 26px;
  font-weight: 800;
  color: #1565c0;
  line-height: 1;
}
.total-val span { font-size: 13px; color: #607090; font-weight: 400; }
.total-lbl { font-size: 11px; color: #607090; margin-top: 2px; }
.total-grade {
  display: inline-block;
  margin-top: 5px;
  padding: 2px 10px;
  border-radius: 12px;
  font-size: 11px;
  font-weight: 700;
}
.grade-a { background: #e8f5e9; color: #2e7d32; }

.criteria-list { display: flex; flex-direction: column; gap: 9px; }

.criterion-row {}
.crit-top {
  display: flex;
  align-items: center;
  margin-bottom: 3px;
}
.crit-label { flex: 1; font-size: 11px; color: #2c3345; font-weight: 500; }
.crit-weight { font-size: 10px; color: #90a0b8; margin-right: 6px; }
.crit-score { font-size: 12px; font-weight: 700; min-width: 34px; text-align: right; }

.bar-bg {
  height: 6px;
  background: #eef1f7;
  border-radius: 3px;
  overflow: hidden;
}
.bar-fill {
  height: 100%;
  border-radius: 3px;
  transition: width 0.6s ease;
}
</style>
