<script setup>
const sopDoc = {
  id: 'GT-2A-001',
  title: 'Gate Layer Type 2A 결함 분류 기준',
  version: 'Rev.3',
  updated: '2025-11-15',
}

const conditions = [
  { seq: 1, category: '발생 Layer',    condition: 'GATE (GT-xxx)',                  result: '적용' },
  { seq: 2, category: '결함 Type',     condition: 'Particle / Foreign Material',    result: '적용' },
  { seq: 3, category: '결함 크기',     condition: '0.20 μm ≤ Size ≤ 0.50 μm',     result: '적용' },
  { seq: 4, category: 'Process',       condition: 'Dry Etch / KRF',                result: '적용' },
  { seq: 5, category: '위치',          condition: 'Active area (주요 패턴 위)',       result: '적용' },
  { seq: 6, category: '후속 처리',     condition: 'ADC 자동 처리 대상',              result: '적용' },
]

const relatedSOP = [
  { id: 'GT-2B-001', desc: 'Gate Layer Type 2B – 크기 0.5μm 초과', link: true },
  { id: 'GT-1A-001', desc: 'Gate Layer Type 1A – Scratch 유형', link: true },
]
</script>

<template>
  <div class="panel">
    <div class="panel-header">
      <span class="badge-num">⑥</span>
      <span class="panel-title">SOP / 세부 근거 정보</span>
    </div>

    <div class="body">
      <div class="sop-meta">
        <div class="sop-id-block">
          <span class="sop-id">{{ sopDoc.id }}</span>
          <span class="sop-ver">{{ sopDoc.version }}</span>
        </div>
        <div class="sop-title">{{ sopDoc.title }}</div>
        <div class="sop-date">최종 업데이트: {{ sopDoc.updated }}</div>
      </div>

      <table class="cond-table">
        <thead>
          <tr>
            <th>#</th>
            <th>분류 항목</th>
            <th>조건 / 기준</th>
            <th>적용</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="c in conditions" :key="c.seq">
            <td class="seq">{{ c.seq }}</td>
            <td class="cat">{{ c.category }}</td>
            <td class="cond">{{ c.condition }}</td>
            <td><span class="apply-badge">{{ c.result }}</span></td>
          </tr>
        </tbody>
      </table>

      <div class="related-sop">
        <div class="related-title">관련 SOP</div>
        <div v-for="s in relatedSOP" :key="s.id" class="related-row">
          <span class="related-id">{{ s.id }}</span>
          <span class="related-desc">{{ s.desc }}</span>
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

.body { padding: 10px 12px; display: flex; flex-direction: column; gap: 10px; }

.sop-meta {
  background: #f0f4fa;
  border-left: 3px solid #1565c0;
  border-radius: 0 6px 6px 0;
  padding: 8px 10px;
  display: flex;
  flex-direction: column;
  gap: 3px;
}
.sop-id-block { display: flex; gap: 6px; align-items: center; }
.sop-id {
  font-size: 13px; font-weight: 800;
  color: #1565c0;
  font-family: 'Courier New', monospace;
}
.sop-ver {
  font-size: 10px; font-weight: 600;
  color: white; background: #1565c0;
  padding: 1px 6px; border-radius: 3px;
}
.sop-title { font-size: 11px; font-weight: 600; color: #1a2a4a; }
.sop-date { font-size: 10px; color: #90a0b8; }

.cond-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 11px;
}
.cond-table thead th {
  background: #f0f4fa;
  color: #607090;
  font-weight: 600;
  padding: 5px 8px;
  text-align: left;
  font-size: 10px;
  border-bottom: 1px solid #e0e8f0;
}
.cond-table td { padding: 5px 8px; border-bottom: 1px solid #f0f4fa; }
.cond-table .seq { color: #90a0b8; font-size: 10px; text-align: center; width: 24px; }
.cond-table .cat { color: #607090; font-weight: 600; font-size: 10px; white-space: nowrap; }
.cond-table .cond { color: #2c3345; }

.apply-badge {
  display: inline-block;
  background: #e8f5e9;
  color: #2e7d32;
  font-size: 10px;
  font-weight: 600;
  padding: 2px 6px;
  border-radius: 3px;
}

.related-sop {}
.related-title {
  font-size: 10px;
  font-weight: 700;
  color: #607090;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-bottom: 5px;
}
.related-row {
  display: flex;
  gap: 8px;
  align-items: center;
  padding: 4px 0;
  border-bottom: 1px solid #f0f4fa;
  font-size: 10px;
}
.related-id {
  color: #1565c0;
  font-weight: 700;
  font-family: 'Courier New', monospace;
  cursor: pointer;
  text-decoration: underline;
  white-space: nowrap;
}
.related-desc { color: #607090; }
</style>
