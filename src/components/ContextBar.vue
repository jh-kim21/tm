<script setup>
const fields = [
  { label: 'Device',      value: 'D128M' },
  { label: 'Lot',         value: 'LOT20260715-001' },
  { label: 'Wafer',       value: 'W12' },
  { label: 'Layer',       value: 'M3' },
  { label: 'Mask',        value: 'M3A' },
  { label: 'Process',     value: 'P120' },
  { label: 'Defect ID',   value: 'D-10293' },
  { label: 'Review Step', value: 'Final Judge' },
]
</script>

<template>
  <div class="context-bar">
    <div class="field" v-for="f in fields" :key="f.label">
      <span class="label">{{ f.label }}</span>
      <span class="value">{{ f.value }}</span>
    </div>
    <div class="nav-btns">
      <button class="nav-btn">‹ Prev</button>
      <button class="nav-btn">Next ›</button>
    </div>
  </div>
</template>

<style scoped>
.context-bar {
  display: flex;
  align-items: center;
  gap: 24px;
  padding: 8px 16px;
  background: white;
  border-bottom: 1px solid #e4e9f0;
  box-shadow: 0 1px 4px rgba(0,0,0,0.04);
  flex-wrap: wrap;
}

.field {
  display: flex;
  flex-direction: column;
  gap: 1px;
}

.label {
  font-size: 9px;
  color: #90a0b8;
  text-transform: uppercase;
  letter-spacing: 0.4px;
}

.value {
  font-size: 12px;
  font-weight: 700;
  color: #1a2a4a;
}

.nav-btns {
  margin-left: auto;
  display: flex;
  gap: 6px;
}

.nav-btn {
  padding: 5px 12px;
  border: 1px solid #d0d8e8;
  background: white;
  color: #4a5a72;
  border-radius: 5px;
  font-size: 11px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.15s;
}
.nav-btn:hover { border-color: #1565c0; color: #1565c0; }

@media print {
  .context-bar { padding: 4px 10px; gap: 12px; }
  .label { font-size: 8px; }
  .value { font-size: 10px; }
  .nav-btns { display: none; }
}
</style>
