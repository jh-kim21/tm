<script setup>
import NavHeader from '../components/NavHeader.vue'
import WaferDefectPanel from '../components/WaferDefectPanel.vue'
import AIRecommendationPanel from '../components/AIRecommendationPanel.vue'
import ScoreBreakdownPanel from '../components/ScoreBreakdownPanel.vue'
import EvidencePanel from '../components/EvidencePanel.vue'
import SimilarMaskTable from '../components/SimilarMaskTable.vue'
import SOPPanel from '../components/SOPPanel.vue'
import AuditTrailPanel from '../components/AuditTrailPanel.vue'
</script>

<template>
  <div class="page">
    <NavHeader />
    <div class="content-grid">
      <section class="area-wfr">
        <WaferDefectPanel />
      </section>
      <section class="area-ai">
        <AIRecommendationPanel />
      </section>
      <section class="area-score">
        <ScoreBreakdownPanel />
      </section>
      <section class="area-evi">
        <EvidencePanel />
      </section>
      <section class="area-similar">
        <SimilarMaskTable />
      </section>
      <section class="area-sop">
        <SOPPanel />
      </section>
      <section class="area-audit">
        <AuditTrailPanel />
      </section>
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
  display: grid;
  grid-template-columns: 255px 1fr 290px;
  grid-template-rows: auto auto auto auto;
  grid-template-areas:
    "wfr  ai      score"
    "wfr  evi     score"
    "wfr  similar audit"
    "wfr  sop     audit";
  gap: 8px;
  padding: 8px;
  flex: 1;
}

.area-wfr     { grid-area: wfr; }
.area-ai      { grid-area: ai; }
.area-score   { grid-area: score; }
.area-evi     { grid-area: evi; }
.area-similar { grid-area: similar; }
.area-sop     { grid-area: sop; }
.area-audit   { grid-area: audit; }
</style>
