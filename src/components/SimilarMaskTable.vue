<script setup>
import simcase1 from '../assets/defect-images/simcase-1.png'
import simcase2 from '../assets/defect-images/simcase-2.png'
import simcase3 from '../assets/defect-images/simcase-3.png'
import simcase4 from '../assets/defect-images/simcase-4.png'
import simcase5 from '../assets/defect-images/simcase-5.png'

const rows = [
  {
    rank: 1, score: 98.1, code: '2A', img: simcase1,
    layerMaskDevice: 'M3 / M3A / D128M',
    same: 'Layer, Mask, Pattern\nSize 유사',
    comment: 'Pattern edge hairline.\nCustomer 기준상 2A 처리.',
    date: '2026-06-21',
    highlight: false,
  },
  {
    rank: 2, score: 97.4, code: '2A', img: simcase2,
    layerMaskDevice: 'M3 / M3A / D128M',
    same: 'Layer, Mask,  Device\nPattern 유사',
    comment: '동일 조건 재발 사례.\n2A 유지.',
    date: '2026-06-18',
    highlight: false,
  },
  {
    rank: 3, score: 95.9, code: '2A', img: simcase3,
    layerMaskDevice: 'M3 / M3A / D128M',
    same: 'Layer, Mask 동일\nSize 유사',
    comment: 'Hairline 유형. 영향 없음.',
    date: '2026-06-15',
    highlight: false,
  },
  {
    rank: 4, score: 94.8, code: '2B', img: simcase4,
    layerMaskDevice: 'M3 / M3A / D128M',
    same: 'Layer, Mask 동일\nPattern 유사',
    comment: '크기가 커서 2B 처리.',
    date: '2026-06-10',
    highlight: true,
  },
  {
    rank: 5, score: 93.7, code: '2A', img: simcase5,
    layerMaskDevice: 'M3 / M3A / D256M',
    same: 'Mask, Pattern 유사',
    comment: '유사하나 Device 다름.',
    date: '2026-06-08',
    highlight: false,
  },
]
</script>

<template>
  <div class="panel">
    <div class="panel-header">
      <span class="badge-num">⑤</span>
      <span class="panel-title">유사사례 Top 5</span>
    </div>

    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>Rank</th>
            <th>유사도</th>
            <th>Final Code</th>
            <th>Layer / Mask / Device</th>
            <th>같은 점 (주요)</th>
            <th>Engineer Comment</th>
            <th>Date</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="r in rows" :key="r.rank" :class="{ 'row-highlight': r.highlight }">
            <td>
              <div class="rank-cell">
                <span class="rank-num">{{ r.rank }}</span>
                <div class="thumb-cell">
                  <img :src="r.img" :alt="`similar case rank ${r.rank}`"/>
                  <svg v-if="r.highlight" class="thumb-cell-overlay" viewBox="0 0 60 44" preserveAspectRatio="none">
                    <rect x="24" y="16" width="14" height="12" fill="none" stroke="#f44336" stroke-width="1" stroke-dasharray="2,1.5"/>
                    <line x1="12" y1="22" x2="48" y2="22" stroke="#f44336" stroke-width="0.5" opacity="0.6"/>
                  </svg>
                </div>
              </div>
            </td>
            <td>
              <div class="sim-row">
                <div class="mini-bar">
                  <div :style="{ width: r.score + '%', background: r.highlight ? '#ff9800' : '#42a5f5' }"/>
                </div>
                <span class="sim-pct">{{ r.score }}%</span>
              </div>
            </td>
            <td>
              <span :class="['code-chip', r.code === '2A' ? 'c2a' : 'c2b']">{{ r.code }}</span>
            </td>
            <td class="td-mono">{{ r.layerMaskDevice }}</td>
            <td class="td-multiline">{{ r.same }}</td>
            <td class="td-multiline td-comment">{{ r.comment }}</td>
            <td class="td-date">{{ r.date }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="table-footer">
      <button class="more-btn">더 많은 유사사례 보기 (50건)</button>
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
.panel-title { font-size: 12px; font-weight: 700; color: #1a2a4a; flex: 1; }

.table-wrap { overflow: auto; flex: 1; }

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
tbody tr.row-highlight {
  background: #fff8f0;
  box-shadow: inset 0 0 0 1.5px #ffb74d;
}

td { padding: 6px 8px; vertical-align: middle; }

.rank-cell {
  display: flex;
  align-items: center;
  gap: 6px;
}
.rank-num { font-size: 11px; font-weight: 700; color: #607090; width: 12px; }

.thumb-cell { position: relative; width: 60px; height: 44px; line-height: 0; }
.thumb-cell img { width: 60px; height: 44px; border-radius: 3px; display: block; object-fit: cover; }
.thumb-cell-overlay { position: absolute; inset: 0; width: 100%; height: 100%; }

.td-mono { font-family: 'Courier New', monospace; font-size: 10px; color: #2c3345; white-space: nowrap; }

.code-chip {
  display: inline-block;
  padding: 2px 7px;
  border-radius: 3px;
  font-size: 11px;
  font-weight: 700;
}
.code-chip.c2a { background: #e8f5e9; color: #2e7d32; }
.code-chip.c2b { background: #fff3e0; color: #ef6c00; }

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

.td-multiline { color: #2c3345; font-size: 10px; white-space: pre-line; max-width: 150px; }
.td-comment { color: #607090; max-width: 160px; }
.td-date { color: #90a0b8; font-size: 10px; white-space: nowrap; }

.table-footer {
  padding: 8px 12px;
  border-top: 1px solid #eef1f7;
  display: flex;
  justify-content: center;
}
.more-btn {
  padding: 6px 16px;
  border: 1px solid #d0d8e8;
  background: white;
  color: #4a5a72;
  border-radius: 5px;
  font-size: 11px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.15s;
}
.more-btn:hover { border-color: #1565c0; color: #1565c0; }

@media print {
  .panel-header { padding: 4px 8px 3px; }
  .badge-num { width: 14px; height: 14px; font-size: 9px; }
  .panel-title { font-size: 10px; }
  thead th { padding: 4px 6px; }
  td { padding: 4px 6px; }
  .thumb-cell, .thumb-cell img { width: 42px; height: 30px; }
  .table-footer { display: none; }
}
</style>
