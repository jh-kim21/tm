<script setup>
import NavHeader from '../components/NavHeader.vue'
import ContextBar from '../components/ContextBar.vue'
import WaferDefectPanel from '../components/WaferDefectPanel.vue'
import AIScorePanel from '../components/AIScorePanel.vue'
import ScoreBreakdownPanel from '../components/ScoreBreakdownPanel.vue'
import EvidencePanel from '../components/EvidencePanel.vue'
import SimilarMaskTable from '../components/SimilarMaskTable.vue'
import SOPPanel from '../components/SOPPanel.vue'
import AuditTrailPanel from '../components/AuditTrailPanel.vue'
</script>

<template>
  <div class="page">
    <NavHeader />
    <ContextBar />
    <div class="content-grid">
      <div class="row row-1">
        <section class="col-wfr"><WaferDefectPanel /></section>
        <section class="col-aisc"><AIScorePanel /></section>
        <section class="col-score"><ScoreBreakdownPanel /></section>
      </div>
      <div class="row row-2">
        <section class="col-evi"><EvidencePanel /></section>
      </div>
      <div class="row row-3">
        <section class="col-similar"><SimilarMaskTable /></section>
        <section class="col-sop"><SOPPanel /></section>
        <section class="col-audit"><AuditTrailPanel /></section>
      </div>
    </div>
  </div>
</template>

<style scoped>
.page {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.content-grid {
  display: flex;
  flex-direction: column;
  gap: 12px;
  padding: 12px;
  flex: 1;
}

.row {
  display: flex;
  gap: 12px;
  align-items: stretch;
}

.row-1 { flex: 1.55; min-height: 0; }
.row-2 { flex: 1; min-height: 0; }
.row-3 { flex: 1.4; min-height: 0; }

.col-wfr   { flex: 49; min-width: 0; }
.col-aisc  { flex: 27; min-width: 0; }
.col-score { flex: 24; min-width: 0; }

.col-evi { flex: 1; min-width: 0; }

.col-similar { flex: 62; min-width: 0; }
.col-sop     { flex: 19; min-width: 0; }
.col-audit   { flex: 19; min-width: 0; }

@media print {
  @page { size: landscape; margin: 8mm; }
  .content-grid { gap: 6px; padding: 6px; }
  .row { gap: 6px; }
}
</style>
