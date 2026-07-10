<script setup>
const rows = [
  {
    rank: 1, score: 98.1,
    device: 'D30V-A', layer: 'KRF-GATE', maskProcess: 'Dry',
    code: '2A', result: 'Pass', comment: '판정기준 참조',
    imgColor: '#0a1a2a',
  },
  {
    rank: 2, score: 95.3,
    device: 'D30V-A', layer: 'KRF-GATE', maskProcess: 'Dry',
    code: '2A', result: 'Pass', comment: 'ADC 자동 처리',
    imgColor: '#0a1a2a',
  },
  {
    rank: 3, score: 91.7,
    device: 'D20-B', layer: 'ArF-METAL', maskProcess: 'Wet',
    code: '2B', result: 'Fail', comment: 'Rework 필요',
    imgColor: '#0a1a2a',
  },
  {
    rank: 4, score: 88.4,
    device: 'D20-B', layer: 'ArF-POLY', maskProcess: 'Dry',
    code: '2A', result: 'Pass', comment: '-',
    imgColor: '#0a1a2a',
  },
  {
    rank: 5, score: 84.2,
    device: 'D30V-A', layer: 'KRF-CONTACT', maskProcess: 'Dry',
    code: '3A', result: 'Scrap', comment: '특이사항 없음',
    imgColor: '#0a1a2a',
  },
]
</script>

<template>
  <div class="panel">
    <div class="panel-header">
      <span class="badge-num">⑤</span>
      <span class="panel-title">유사마스크 Top 5</span>
      <span class="header-note">DEF-042 기준 | 유사도 순 정렬</span>
    </div>

    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>순위</th>
            <th>이미지</th>
            <th>Device</th>
            <th>Layer / Video Name</th>
            <th>Mask Process</th>
            <th>결함코드</th>
            <th>유사도</th>
            <th>실제 결과</th>
            <th>Engineer Comment</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="r in rows" :key="r.rank" :class="{ 'row-top': r.rank === 1 }">
            <td>
              <div :class="['rank-badge', r.rank === 1 ? 'rank-1' : r.rank === 2 ? 'rank-2' : r.rank === 3 ? 'rank-3' : 'rank-n']">
                {{ r.rank }}
              </div>
            </td>
            <td>
              <div class="thumb-cell">
                <svg viewBox="0 0 48 36">
                  <rect width="48" height="36" :fill="r.imgColor"/>
                  <rect x="0" y="8" width="48" height="5" fill="#0e2235"/>
                  <rect x="0" y="23" width="48" height="5" fill="#0e2235"/>
                  <line x1="0" y1="8" x2="48" y2="8" stroke="#2a6a9a" stroke-width="0.7"/>
                  <line x1="0" y1="13" x2="48" y2="13" stroke="#2a6a9a" stroke-width="0.7"/>
                  <line x1="0" y1="23" x2="48" y2="23" stroke="#2a6a9a" stroke-width="0.7"/>
                  <line x1="0" y1="28" x2="48" y2="28" stroke="#2a6a9a" stroke-width="0.7"/>
                  <circle cx="24" cy="17" r="4"
                    :fill="r.result === 'Pass' ? '#1565c0' : r.result === 'Fail' ? '#e53935' : '#7b1fa2'"
                    opacity="0.8"/>
                </svg>
              </div>
            </td>
            <td class="td-mono">{{ r.device }}</td>
            <td class="td-mono">{{ r.layer }}</td>
            <td>
              <span :class="['process-tag', r.maskProcess === 'Dry' ? 'dry' : 'wet']">
                {{ r.maskProcess }}
              </span>
            </td>
            <td>
              <span :class="['code-chip', r.code === '2A' ? 'c2a' : r.code === '2B' ? 'c2b' : 'c3a']">
                {{ r.code }}
              </span>
            </td>
            <td>
              <div class="sim-row">
                <div class="mini-bar">
                  <div :style="{ width: r.score + '%', background: r.rank === 1 ? '#1565c0' : '#42a5f5' }"/>
                </div>
                <span class="sim-pct">{{ r.score }}%</span>
              </div>
            </td>
            <td>
              <span :class="['result-tag', r.result === 'Pass' ? 'pass' : r.result === 'Fail' ? 'fail' : 'scrap']">
                {{ r.result }}
              </span>
            </td>
            <td class="td-comment">{{ r.comment }}</td>
          </tr>
        </tbody>
      </table>
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
.panel-title { font-size: 12px; font-weight: 700; color: #1a2a4a; flex: 1; }
.header-note { font-size: 10px; color: #90a0b8; }

.table-wrap { overflow-x: auto; }

table {
  width: 100%;
  border-collapse: collapse;
  font-size: 11px;
}

thead th {
  background: #f0f4fa;
  color: #607090;
  font-weight: 600;
  padding: 6px 8px;
  text-align: left;
  font-size: 10px;
  white-space: nowrap;
  border-bottom: 1px solid #e0e8f0;
}

tbody tr {
  border-bottom: 1px solid #f0f4fa;
  transition: background 0.1s;
}
tbody tr:hover { background: #f8fafd; }
tbody tr.row-top { background: #fafbff; }

td { padding: 6px 8px; vertical-align: middle; }

.rank-badge {
  width: 22px; height: 22px;
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 11px; font-weight: 700;
}
.rank-1 { background: #ffd700; color: #7b5e00; }
.rank-2 { background: #e0e0e0; color: #4a4a4a; }
.rank-3 { background: #cd7f32; color: white; }
.rank-n { background: #f0f4fa; color: #607090; }

.thumb-cell svg { width: 48px; height: 36px; border-radius: 3px; display: block; }

.td-mono { font-family: 'Courier New', monospace; font-size: 10px; color: #2c3345; }

.process-tag {
  display: inline-block;
  padding: 2px 6px;
  border-radius: 3px;
  font-size: 10px;
  font-weight: 600;
}
.process-tag.dry { background: #e3f2fd; color: #1565c0; }
.process-tag.wet { background: #e8f5e9; color: #2e7d32; }

.code-chip {
  display: inline-block;
  padding: 2px 7px;
  border-radius: 3px;
  font-size: 11px;
  font-weight: 700;
}
.code-chip.c2a { background: #e3f2fd; color: #1565c0; }
.code-chip.c2b { background: #fff8e1; color: #f57f17; }
.code-chip.c3a { background: #fce4ec; color: #c62828; }

.sim-row {
  display: flex;
  align-items: center;
  gap: 5px;
}
.mini-bar {
  width: 50px; height: 5px;
  background: #e8edf4;
  border-radius: 3px;
  overflow: hidden;
}
.mini-bar div { height: 100%; border-radius: 3px; }
.sim-pct { font-size: 10px; font-weight: 600; color: #1565c0; white-space: nowrap; }

.result-tag {
  display: inline-block;
  padding: 2px 7px;
  border-radius: 3px;
  font-size: 10px;
  font-weight: 600;
}
.result-tag.pass  { background: #e8f5e9; color: #2e7d32; }
.result-tag.fail  { background: #ffebee; color: #c62828; }
.result-tag.scrap { background: #f3e5f5; color: #7b1fa2; }

.td-comment { color: #607090; font-size: 10px; max-width: 120px; }
</style>
