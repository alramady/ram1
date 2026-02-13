# 9. كود Vue/Vuexy المرجعي

تعرض صفحة تنفيذ الفحص كود Vue/Vuexy كمرجع تصميمي. هذا الكود يمثل الهدف النهائي للتنفيذ باستخدام إطار عمل Vue.js مع قالب Vuexy.

## 9.1. الكود الكامل (ScanExecution.vue)

```vue
<!-- ScanExecution.vue -->
<template>
  <div class="scan-execution" :class="{ 'dark': isDark }">
    <!-- Header Banner -->
    <div class="scan-header glass-card">
      <div class="flex items-center gap-4">
        <div class="scan-icon" :class="{ 'animate-spin': isRunning }">
          <ShieldIcon />
        </div>
        <div>
          <h2>محرك راصد للفحص المتقدم</h2>
          <p>راصد - عين المملكة الرقابية على حماية الخصوصية</p>
        </div>
      </div>
      
      <!-- Progress Bar -->
      <div class="progress-container mt-4">
        <div class="progress-bar" :style="{ width: progress + '%' }">
          <div v-if="isRunning" class="shimmer-effect" />
        </div>
      </div>
    </div>

    <!-- Tabs -->
    <VTabs v-model="activeTab">
      <VTab value="log">السجل</VTab>
      <VTab value="stages">المراحل</VTab>
      <VTab value="article12">المادة 12</VTab>
      <VTab value="screenshot">لقطة</VTab>
    </VTabs>

    <!-- Log Panel -->
    <div v-if="activeTab === 'log'" class="log-panel" ref="logRef">
      <div v-for="log in logs" :key="log.id" class="log-entry"
           :class="'log-' + log.type">
        <span class="log-time">{{ log.time }}</span>
        <component :is="getLogIcon(log.type)" :size="14" />
        <span>{{ log.message }}</span>
      </div>
    </div>

    <!-- Article 12 Panel -->
    <div v-if="activeTab === 'article12'" class="article12-panel">
      <div v-for="item in article12Items" :key="item.id"
           class="article12-item" :class="'status-' + item.status">
        <component :is="getStatusIcon(item.status)" :size="16" />
        <div>
          <p class="font-medium">البند {{ item.id }}: {{ item.title }}</p>
          <p class="text-xs opacity-60">{{ item.details }}</p>
        </div>
        <VChip :color="item.status === 'compliant' ? 'success' : 'warning'"
               size="small">
          {{ item.status === 'compliant' ? 'مكتمل' : 'غير مكتمل' }}
        </VChip>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, watch, nextTick } from 'vue'
import { useSoundEffects } from '@/composables/useSoundEffects'

const { playClick, playScanStart, playStageComplete } = useSoundEffects()

const isRunning = ref(false)
const progress = ref(0)
const activeTab = ref('log')
const logs = ref([])
const logRef = ref(null)

// Auto-scroll log
watch(logs, async () => {
  await nextTick()
  if (logRef.value) logRef.value.scrollTop = logRef.value.scrollHeight
}, { deep: true })

const startScan = () => {
  isRunning.value = true
  playScanStart()
  // ... simulation logic
}
</script>

<style scoped>
.scan-execution {
  font-family: 'Tajawal', sans-serif;
  direction: rtl;
}

.glass-card {
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(39, 52, 112, 0.1);
  border-radius: 1rem;
}

.dark .glass-card {
  background: rgba(39, 52, 112, 0.25);
  border-color: rgba(30, 58, 95, 0.12);
}

.progress-bar {
  height: 12px;
  border-radius: 9999px;
  background: linear-gradient(90deg, #1E3A5F, #6459A7);
  transition: width 0.5s ease;
}

.shimmer-effect {
  position: absolute;
  inset: 0;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
  animation: shimmer 1.5s linear infinite;
}

.log-entry {
  display: flex;
  align-items: start;
  gap: 0.75rem;
  padding: 0.375rem 0.5rem;
}

.log-success { color: #1E3A5F; }
.log-warning { color: #FFC107; }
.log-error   { color: #EB3D63; }
.log-stage   { color: #6459A7; background: rgba(100, 89, 167, 0.05); border-radius: 0.5rem; }
</style>
```
