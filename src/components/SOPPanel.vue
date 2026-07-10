<script setup>
import { ref } from 'vue'

const activeTab = ref('mail')

const mail = {
  subject: '[Rule Update] M3 Layer Hairline Defect 판정 기준 변경',
  sentDate: '2026-06-28',
  author: 'Process Engineering Team',
  approver: 'Quality Manager',
  effectiveDate: '2026-07-01',
  body: '"고객 요청에 따라 M3 Layer Hairline Defect는\n기존 2B가 아닌 2A로 처리한다.\n해당 변경은 2026-07-01 이후 발생하는 Lot부터 적용한다."',
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
      <span class="panel-title">SOP / 메일 근거 원문</span>
    </div>

    <div class="tabs">
      <button :class="['tab-btn', { active: activeTab === 'mail' }]" @click="activeTab = 'mail'">Mail</button>
      <button :class="['tab-btn', { active: activeTab === 'sop' }]" @click="activeTab = 'sop'">SOP</button>
    </div>

    <div class="body" v-if="activeTab === 'mail'">
      <table class="mail-meta">
        <tbody>
          <tr><td class="mkey">제목</td><td class="mval">{{ mail.subject }}</td></tr>
          <tr><td class="mkey">발신일</td><td class="mval">{{ mail.sentDate }}</td></tr>
          <tr><td class="mkey">작성자</td><td class="mval">{{ mail.author }}</td></tr>
          <tr><td class="mkey">승인자</td><td class="mval">{{ mail.approver }}</td></tr>
          <tr><td class="mkey">적용일</td><td class="mval">{{ mail.effectiveDate }}</td></tr>
        </tbody>
      </table>

      <div class="mail-body-section">
        <div class="mail-body-title">원문 내용</div>
        <div class="mail-body-text">{{ mail.body }}</div>
      </div>

      <div class="ev-btn-row">
        <button class="ev-btn">전체 원문 보기</button>
        <button class="ev-btn">관련 Defect 사례 보기</button>
      </div>
    </div>

    <div class="body" v-else>
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
  height: 100%;
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

.tabs {
  display: flex;
  gap: 4px;
  padding: 6px 12px 0;
  border-bottom: 1px solid #eef1f7;
}
.tab-btn {
  padding: 6px 14px;
  border: none;
  background: none;
  color: #90a0b8;
  font-size: 11px;
  font-weight: 600;
  cursor: pointer;
  border-bottom: 2px solid transparent;
}
.tab-btn.active { color: #1565c0; border-bottom-color: #1565c0; }

.body { padding: 10px 12px; display: flex; flex-direction: column; gap: 10px; flex: 1; overflow: auto; }

.mail-meta {
  width: 100%;
  border-collapse: collapse;
  font-size: 11px;
}
.mail-meta tr { border-bottom: 1px solid #f0f4fa; }
.mail-meta tr:last-child { border-bottom: none; }
.mkey {
  width: 54px;
  color: #90a0b8;
  padding: 4px 8px 4px 0;
  vertical-align: top;
  white-space: nowrap;
}
.mval { color: #1a2a4a; font-weight: 600; padding: 4px 0; }

.mail-body-section {
  background: #f0f4fa;
  border-left: 3px solid #1565c0;
  border-radius: 0 6px 6px 0;
  padding: 8px 10px;
}
.mail-body-title {
  font-size: 10px;
  font-weight: 700;
  color: #607090;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-bottom: 5px;
}
.mail-body-text {
  font-size: 11px;
  color: #2c3345;
  white-space: pre-line;
  line-height: 1.6;
}

.ev-btn-row { display: flex; gap: 6px; margin-top: auto; }
.ev-btn {
  flex: 1;
  padding: 6px 8px;
  border: 1px solid #d0d8e8;
  background: white;
  color: #1565c0;
  border-radius: 4px;
  font-size: 10.5px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.15s;
}
.ev-btn:hover { background: #e3f2fd; border-color: #1565c0; }

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
