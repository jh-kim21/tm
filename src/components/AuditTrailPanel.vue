<script setup>
import { ref } from 'vue'

const selectedCode = ref('2A')
const selectedGrade = ref('3')
const comment = ref('')
const submitted = ref(false)

const codeOptions = ['1A', '1B', '2A', '2B', '3A', '3B', 'SKIP']
const gradeOptions = ['1', '2', '3', '4', 'Scrap']

const auditLog = ref([
  {
    time: '2026-07-15 10:21',
    actor: 'AI System',
    action: 'AI Recommendation',
    detail: 'Code: 2A (91.8%)',
    type: 'ai',
  },
  {
    time: '2026-07-15 10:22',
    actor: 'Eng. Kim',
    action: 'Engineer Review',
    detail: 'Code: 2A',
    type: 'user',
  },
  {
    time: '2026-07-15 10:25',
    actor: 'Eng. Kim',
    action: 'Final Judge',
    detail: 'Code: 2A',
    type: 'judge',
  },
  {
    time: '2026-07-15 10:25',
    actor: 'Eng. Kim',
    action: 'Comment 입력',
    detail: '"유사사례 및 SOP 근거 확인 후 2A 결정."',
    type: 'user',
  },
  {
    time: '2026-07-15 10:26',
    actor: 'Eng. Kim',
    action: 'Approve',
    detail: 'Engineer Kim',
    type: 'judge',
  },
])

function submit() {
  if (!comment.value.trim()) return
  auditLog.value.push({
    time: new Date().toLocaleTimeString('ko-KR', { hour12: false }),
    actor: 'Eng. Kim',
    action: `판정 확정 [${selectedCode.value}]`,
    detail: comment.value,
    type: 'judge',
  })
  submitted.value = true
}
</script>

<template>
  <div class="panel">
    <div class="panel-header">
      <span class="badge-num">⑦</span>
      <span class="panel-title">판정 이력 <span class="sub">& Audit Trail</span></span>
    </div>

    <div class="body">
      <!-- Judgment form -->
      <div class="form-section">
        <div class="form-title">판정 입력</div>

        <div class="form-row">
          <label>결함 코드</label>
          <div class="code-selector">
            <button v-for="c in codeOptions" :key="c"
              :class="['code-btn', { active: selectedCode === c }]"
              @click="selectedCode = c">
              {{ c }}
            </button>
          </div>
        </div>

        <div class="form-row">
          <label>결함 등급</label>
          <div class="code-selector">
            <button v-for="g in gradeOptions" :key="g"
              :class="['grade-btn', { active: selectedGrade === g }]"
              @click="selectedGrade = g">
              {{ g }}
            </button>
          </div>
        </div>

        <div class="form-row ai-suggest">
          <span class="ai-icon">AI</span>
          <span>추천: <b>{{ selectedCode }}</b> · 등급 <b>{{ selectedGrade }}</b></span>
          <span class="conf">91.8%</span>
        </div>

        <div class="form-row">
          <label>판정 의견</label>
          <textarea v-model="comment"
            placeholder="판정 근거 또는 특이사항을 입력하세요..."
            :disabled="submitted"
            rows="3"/>
        </div>

        <button class="submit-btn"
          :class="{ submitted }"
          :disabled="submitted || !comment.trim()"
          @click="submit">
          <template v-if="submitted">✓ 판정 완료</template>
          <template v-else>판정 확정</template>
        </button>
      </div>

      <!-- Audit Trail log -->
      <div class="audit-section">
        <div class="form-title">Audit Trail</div>
        <div class="log-list">
          <div v-for="(log, i) in auditLog" :key="i"
            :class="['log-entry', log.type]">
            <div class="log-left">
              <div :class="['log-dot', log.type]"/>
              <div v-if="i < auditLog.length - 1" class="log-line"/>
            </div>
            <div class="log-content">
              <div class="log-top">
                <span :class="['log-actor', log.type]">{{ log.actor }}</span>
                <span class="log-time">{{ log.time }}</span>
              </div>
              <div class="log-action">{{ log.action }}</div>
              <div class="log-detail">{{ log.detail }}</div>
            </div>
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
.panel-title .sub { font-weight: 400; color: #607090; }

.body {
  padding: 10px 12px;
  display: flex;
  flex-direction: column;
  gap: 12px;
  overflow-y: auto;
  flex: 1;
}

.form-section {
  display: flex;
  flex-direction: column;
  gap: 9px;
}

.form-title {
  font-size: 10px;
  font-weight: 700;
  color: #607090;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  padding-bottom: 4px;
  border-bottom: 1px solid #eef1f7;
}

.form-row {
  display: flex;
  flex-direction: column;
  gap: 4px;
}
.form-row label {
  font-size: 10px;
  font-weight: 600;
  color: #607090;
}

.code-selector {
  display: flex;
  flex-wrap: wrap;
  gap: 4px;
}

.code-btn, .grade-btn {
  padding: 3px 8px;
  border: 1.5px solid #d0d8e8;
  border-radius: 4px;
  background: white;
  color: #4a5a72;
  font-size: 11px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.15s;
}
.code-btn:hover, .grade-btn:hover {
  border-color: #1565c0;
  color: #1565c0;
}
.code-btn.active {
  background: #1565c0;
  border-color: #1565c0;
  color: white;
}
.grade-btn.active {
  background: #ff9800;
  border-color: #ff9800;
  color: white;
}

.ai-suggest {
  display: flex !important;
  flex-direction: row !important;
  align-items: center;
  gap: 6px;
  background: #e3f2fd;
  border-radius: 5px;
  padding: 6px 9px;
  font-size: 11px;
  color: #1a2a4a;
}
.ai-icon {
  background: #1565c0;
  color: white;
  font-size: 9px;
  font-weight: 800;
  padding: 1px 5px;
  border-radius: 3px;
}
.ai-suggest b { color: #1565c0; }
.conf {
  margin-left: auto;
  font-size: 11px;
  font-weight: 700;
  color: #ff9800;
}

textarea {
  width: 100%;
  border: 1.5px solid #d0d8e8;
  border-radius: 5px;
  padding: 7px 9px;
  font-size: 11px;
  font-family: inherit;
  color: #2c3345;
  resize: none;
  outline: none;
  transition: border-color 0.15s;
}
textarea:focus { border-color: #1565c0; }
textarea:disabled { background: #f8fafd; color: #90a0b8; }

.submit-btn {
  width: 100%;
  padding: 9px;
  background: #1565c0;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 13px;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.15s;
  letter-spacing: 0.3px;
}
.submit-btn:hover:not(:disabled) { background: #0d47a1; }
.submit-btn:disabled { opacity: 0.5; cursor: not-allowed; }
.submit-btn.submitted { background: #2e7d32; }

.audit-section { display: flex; flex-direction: column; gap: 8px; }

.log-list { display: flex; flex-direction: column; }

.log-entry {
  display: flex;
  gap: 8px;
  padding: 4px 0;
}

.log-left {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 12px;
  min-width: 12px;
  padding-top: 2px;
}
.log-dot {
  width: 10px; height: 10px;
  border-radius: 50%;
  flex-shrink: 0;
}
.log-dot.ai     { background: #0288d1; }
.log-dot.system { background: #90a0b8; }
.log-dot.user   { background: #ff9800; }
.log-dot.judge  { background: #2e7d32; }

.log-line {
  flex: 1;
  width: 1.5px;
  background: #e0e8f0;
  margin: 2px 0;
  min-height: 12px;
}

.log-content { flex: 1; padding-bottom: 8px; }
.log-top {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1px;
}
.log-actor {
  font-size: 10px;
  font-weight: 700;
}
.log-actor.ai     { color: #0288d1; }
.log-actor.system { color: #90a0b8; }
.log-actor.user   { color: #ff9800; }
.log-actor.judge  { color: #2e7d32; }

.log-time { font-size: 9px; color: #a0b0c0; }
.log-action { font-size: 11px; font-weight: 600; color: #2c3345; }
.log-detail { font-size: 10px; color: #607090; margin-top: 1px; }
</style>
