<script setup>
const navItems = [
  { label: 'Dashboard', active: false },
  { label: 'Defect Guide', active: true },
  { label: 'Search', active: false },
  { label: 'SOP Center', active: false },
  { label: 'Analytics', active: false },
  { label: 'Admin', active: false },
  { label: 'Final Judge', active: false },
]
</script>

<template>
  <header class="nav-header">
    <div class="logo">
      <svg width="22" height="22" viewBox="0 0 22 22" fill="none">
        <polygon points="11,1 20,6 20,16 11,21 2,16 2,6" fill="#4fc3f7" opacity="0.9"/>
        <polygon points="11,4 17,7.5 17,14.5 11,18 5,14.5 5,7.5" fill="#0288d1"/>
        <circle cx="11" cy="11" r="3" fill="white" opacity="0.9"/>
      </svg>
      <span class="logo-text">Klear<b>-view</b></span>
    </div>

    <nav class="nav-items">
      <a v-for="item in navItems" :key="item.label"
         :class="['nav-item', { active: item.active }]">
        {{ item.label }}
      </a>
    </nav>

    <div class="nav-right">
      <button class="icon-btn" title="알림">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
          <path d="M12 22a2 2 0 0 0 2-2H10a2 2 0 0 0 2 2zm6-6V11a6 6 0 0 0-5-5.91V4a1 1 0 0 0-2 0v1.09A6 6 0 0 0 6 11v5l-2 2v1h16v-1l-2-2z"/>
        </svg>
        <span class="badge">3</span>
      </button>
      <div class="user-info">
        <div class="avatar">EK</div>
        <span>Engineer Kim</span>
        <svg width="12" height="12" viewBox="0 0 24 24" fill="currentColor"><path d="M7 10l5 5 5-5z"/></svg>
      </div>
    </div>
  </header>
</template>

<style scoped>
.nav-header {
  display: flex;
  align-items: center;
  gap: 0;
  background: linear-gradient(135deg, #0d1b2e 0%, #1a2a4a 100%);
  height: 50px;
  padding: 0 16px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.3);
  position: sticky;
  top: 0;
  z-index: 100;
}

.logo {
  display: flex;
  align-items: center;
  gap: 8px;
  color: white;
  font-size: 15px;
  font-weight: 500;
  letter-spacing: -0.3px;
  min-width: 150px;
}
.logo b { font-weight: 700; color: #4fc3f7; }
.logo-text { color: #e8eaf6; }

.nav-items {
  display: flex;
  flex: 1;
  gap: 2px;
}

.nav-item {
  padding: 6px 14px;
  color: #90a4c0;
  font-size: 12px;
  font-weight: 500;
  border-radius: 4px;
  cursor: pointer;
  text-decoration: none;
  transition: all 0.15s;
  white-space: nowrap;
}
.nav-item:hover { color: #e0e8f0; background: rgba(255,255,255,0.07); }
.nav-item.active {
  color: #ffffff;
  background: rgba(79, 195, 247, 0.2);
  border-bottom: 2px solid #4fc3f7;
  border-radius: 4px 4px 0 0;
}

.nav-right {
  display: flex;
  align-items: center;
  gap: 12px;
}

.icon-btn {
  position: relative;
  background: none;
  border: none;
  color: #90a4c0;
  cursor: pointer;
  padding: 4px;
  border-radius: 4px;
  display: flex;
  align-items: center;
}
.icon-btn:hover { color: #e0e8f0; background: rgba(255,255,255,0.07); }
.badge {
  position: absolute;
  top: -2px; right: -2px;
  background: #f44336;
  color: white;
  font-size: 9px;
  font-weight: 700;
  width: 14px; height: 14px;
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
}

.user-info {
  display: flex;
  align-items: center;
  gap: 6px;
  color: #c0cfe0;
  font-size: 12px;
  cursor: pointer;
  padding: 4px 8px;
  border-radius: 4px;
}
.user-info:hover { background: rgba(255,255,255,0.07); }
.avatar {
  width: 28px; height: 28px;
  background: linear-gradient(135deg, #4fc3f7, #0288d1);
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 10px; font-weight: 700; color: white;
}
</style>
