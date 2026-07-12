<script setup>
const conditionRows = [
  { field: 'Same Device',      value: 'Yes' },
  { field: 'Same Layer',       value: 'Yes' },
  { field: 'Same Mask Process',value: 'Yes' },
  { field: 'Same WF Process',  value: 'Partial' },
]

const sopRows = [
  { field: '적용 Rule', value: 'M3 Hairline Defect → 2A' },
  { field: '적용일자',  value: '2026-07-01' },
  { field: '출처',      value: 'Engineering Mail / SOP' },
  { field: 'Owner',    value: 'Process Eng. Team' },
]

const distribution = [
  { label: '2A',    count: 44, pct: 88, color: '#2e7d32' },
  { label: '2B',    count: 4,  pct: 8,  color: '#ff9800' },
  { label: 'Hold',  count: 1,  pct: 2,  color: '#fbc02d' },
  { label: 'Other', count: 1,  pct: 2,  color: '#9e9e9e' },
]
</script>

<template>
  <div class="panel">
    <div class="panel-header">
      <span class="badge-num">④</span>
      <span class="panel-title">근거 Evidence 카드</span>
    </div>

    <div class="body">
      <!-- Evidence 1: Image Similarity -->
      <div class="ev-card">
        <div class="ev-title"><span class="ev-dot"/>Evidence 1. 이미지 유사도</div>
        <div class="kv-rows">
          <div class="kv-row"><span class="kv-key">Image Similarity (Top1)</span><span class="kv-val">98.1%</span></div>
          <div class="kv-row"><span class="kv-key">Top 5 평균 유사도</span><span class="kv-val">96.4%</span></div>
        </div>
        <div class="ev-note">유사사례 5건 모두 Final Code 2A</div>
        <div class="ev-btn-row">
          <button class="ev-btn">유사 이미지 보기</button>
          <button class="ev-btn">Overlay 비교</button>
        </div>
      </div>

      <!-- Evidence 2: Same-condition history -->
      <div class="ev-card">
        <div class="ev-title"><span class="ev-dot"/>Evidence 2. 동일 조건 이력</div>
        <div class="kv-rows">
          <div class="kv-row" v-for="c in conditionRows" :key="c.field">
            <span class="kv-key">{{ c.field }}</span><span class="kv-val">{{ c.value }}</span>
          </div>
        </div>
        <div class="ev-note">동일 조건 사례 42건 중 39건이 2A</div>
        <div class="ev-btn-row">
          <button class="ev-btn">조건별 통계 보기</button>
        </div>
      </div>

      <!-- Evidence 3: SOP Rule -->
      <div class="ev-card">
        <div class="ev-title"><span class="ev-dot"/>Evidence 3. SOP Rule</div>
        <div class="kv-rows">
          <div class="kv-row" v-for="s in sopRows" :key="s.field">
            <span class="kv-key">{{ s.field }}</span><span class="kv-val">{{ s.value }}</span>
          </div>
        </div>
        <div class="ev-btn-row">
          <button class="ev-btn">원문 보기</button>
          <button class="ev-btn">관련 SOP 보기</button>
        </div>
      </div>

      <!-- Evidence 4: Final judgment distribution -->
      <div class="ev-card">
        <div class="ev-title"><span class="ev-dot"/>Evidence 4. 최종 판정 분포</div>
        <div class="ev-note">유사사례 50건 기준</div>
        <div class="dist-rows">
          <div class="dist-row" v-for="d in distribution" :key="d.label">
            <span class="dist-label">{{ d.label }}</span>
            <div class="dist-bar-track">
              <div class="dist-bar-fill" :style="{ width: d.pct + '%', background: d.color }"/>
            </div>
            <span class="dist-count">{{ d.count }} ({{ d.pct }}%)</span>
          </div>
        </div>
        <div class="ev-btn-row">
          <button class="ev-btn">분포 상세 보기</button>
        </div>
      </div>

      <!-- Evidence 5: Counter-cases / exceptions -->
      <div class="ev-card">
        <div class="ev-title"><span class="ev-dot"/>Evidence 5. 반대 사례 / 예외</div>
        <div class="ev-note">반대 사례 2건 존재</div>
        <ul class="exception-list">
          <li>2B 판정 사례
            <ul>
              <li>Size 1.8x larger</li>
              <li>Critical Area 위치</li>
            </ul>
          </li>
          <li>ADC 2B 제안 (62.1%)
            <ul>
              <li>해당 조건에서 ADC 오분류율 18%</li>
            </ul>
          </li>
        </ul>
        <div class="ev-btn-row">
          <button class="ev-btn">반대 사례 보기</button>
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
  display: flex; align-items: center; gap: 8px;
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

.body {
  display: flex;
  flex-direction: row;
  align-items: stretch;
  gap: 12px;
  padding: 10px;
  overflow-x: auto;
  flex: 1;
}

.ev-card {
  flex: 1 1 0;
  min-width: 200px;
  background: #f8fafd;
  border: 1px solid #e4e9f4;
  border-radius: 6px;
  padding: 10px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.ev-title {
  font-size: 11.5px;
  font-weight: 700;
  color: #1a2a4a;
  display: flex;
  align-items: center;
  gap: 5px;
}
.ev-dot {
  width: 6px; height: 6px;
  border-radius: 50%;
  background: #1565c0;
  flex-shrink: 0;
}

.kv-rows { display: flex; flex-direction: column; gap: 4px; }
.kv-row {
  display: flex;
  justify-content: space-between;
  gap: 6px;
  font-size: 11px;
}
.kv-key { color: #607090; }
.kv-val { color: #1a2a4a; font-weight: 700; text-align: right; }

.ev-note {
  font-size: 11px;
  color: #4a5a72;
  background: #eef1f7;
  border-radius: 4px;
  padding: 5px 8px;
}

.ev-btn-row {
  display: flex;
  gap: 6px;
  margin-top: auto;
}
.ev-btn {
  flex: 1;
  padding: 6px 6px;
  border: 1px solid #d0d8e8;
  background: white;
  color: #1565c0;
  border-radius: 4px;
  font-size: 10.5px;
  font-weight: 600;
  cursor: pointer;
  white-space: nowrap;
  transition: all 0.15s;
}
.ev-btn:hover { background: #e3f2fd; border-color: #1565c0; }

.dist-rows { display: flex; flex-direction: column; gap: 6px; }
.dist-row {
  display: grid;
  grid-template-columns: 30px 1fr 52px;
  align-items: center;
  gap: 6px;
}
.dist-label { font-size: 10.5px; font-weight: 700; color: #2c3345; }
.dist-bar-track {
  height: 8px;
  background: #eef1f7;
  border-radius: 3px;
  overflow: hidden;
}
.dist-bar-fill { height: 100%; border-radius: 3px; }
.dist-count { font-size: 10.5px; color: #607090; text-align: right; white-space: nowrap; }

.exception-list {
  margin: 0;
  padding-left: 16px;
  font-size: 11px;
  color: #2c3345;
  display: flex;
  flex-direction: column;
  gap: 5px;
}
.exception-list ul {
  margin: 3px 0 0;
  padding-left: 14px;
  color: #607090;
  display: flex;
  flex-direction: column;
  gap: 3px;
}

@media print {
  .panel-header { padding: 4px 8px 3px; }
  .badge-num { width: 14px; height: 14px; font-size: 9px; }
  .panel-title { font-size: 10px; }
  .body { padding: 6px; gap: 6px; }
  .ev-card { padding: 6px; gap: 5px; min-width: 0; }
  .ev-title { font-size: 10px; }
  .ev-btn-row { display: none; }
}
</style>
