<template>
  <section id="projects" class="section">
    <div class="section-inner">
      <h2 class="section-title"><span class="tick"></span>承担课题</h2>
      <div class="proj-list">
        <div v-for="p in projects" :key="p.name" class="proj">
          <div class="proj-top">
            <span class="proj-fund">{{ p.fund }}</span>
            <span class="proj-status" :class="p.status === '在研' ? 'ongoing' : 'done'">{{ p.status }}</span>
          </div>
          <div class="proj-name">{{ p.name }}</div>
          <div class="proj-meta">
            <span>{{ p.period }}</span>
            <span class="proj-role">{{ p.role }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { projects } from '../data/profile.js'
</script>

<style scoped>
.proj-list {
  display: flex;
  flex-direction: column;
  gap: 0;
}
.proj {
  padding: 18px 20px;
  border-bottom: 1px solid var(--line);
  transition: background 0.2s;
}
.proj:hover { background: var(--accent-bg); }
.proj-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  margin-bottom: 8px;
}
.proj-fund {
  color: var(--accent-blue);
  font-size: 14.5px;
  letter-spacing: 0.02em;
}
.proj-status {
  flex-shrink: 0;
  font-size: 13px;
  padding: 2px 10px;
  border: 1px solid;
  border-radius: 999px;
}
.proj-status.done {
  color: var(--ink-dim);
  border-color: var(--line-strong);
}
.proj-status.ongoing {
  color: #166534;
  border-color: #86efac;
  background: #f0fdf4;
}
.proj-name {
  color: var(--ink);
  font-size: 16px;
  line-height: 1.6;
}
.proj-meta {
  margin-top: 8px;
  color: var(--ink-dim);
  font-size: 14px;
  display: flex;
  gap: 14px;
}
.proj-role {
  color: var(--ink-soft);
}
</style>
