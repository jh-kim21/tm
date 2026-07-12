<script setup>
import NavHeader from '../components/NavHeader.vue'
import ContextBar from '../components/ContextBar.vue'
import VerdictBanner from '../components/VerdictBanner.vue'
import WaferDefectPanel from '../components/WaferDefectPanel.vue'
import AIScorePanel from '../components/AIScorePanel.vue'
import EvidencePanel from '../components/EvidencePanel.vue'
import SimilarMaskTable from '../components/SimilarMaskTable.vue'
import SOPPanel from '../components/SOPPanel.vue'
import AuditTrailPanel from '../components/AuditTrailPanel.vue'
</script>

<template>
  <div class="page">
    <NavHeader />
    <ContextBar />
    <VerdictBanner />
    <div class="content-grid">
      <section class="area-wfr">
        <WaferDefectPanel />
      </section>
      <section class="area-aisc">
        <AIScorePanel />
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
  grid-template-columns: repeat(12, 1fr);
  grid-template-rows: auto auto auto;
  grid-template-areas:
    "wfr     wfr     wfr     wfr     wfr     aisc    aisc    aisc    aisc    evi     evi     evi"
    "similar similar similar similar similar similar sop     sop     sop     evi     evi     evi"
    "audit   audit   audit   audit   audit   audit   audit   audit   audit   evi     evi     evi";
  gap: 12px;
  padding: 12px;
  flex: 1;
  align-items: stretch;
}

.area-wfr     { grid-area: wfr; }
.area-aisc    { grid-area: aisc; }
.area-evi     { grid-area: evi; }
.area-similar { grid-area: similar; }
.area-sop     { grid-area: sop; }
.area-audit   { grid-area: audit; }

@media print {
  @page { size: landscape; margin: 8mm; }
  .content-grid { gap: 6px; padding: 6px; }
}
</style>
