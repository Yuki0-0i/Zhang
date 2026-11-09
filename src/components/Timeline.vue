<template>
  <section id="timeline" class="section">
    <div class="section-inner">
      <h2 class="section-title"><span class="tick"></span>学习与工作经历</h2>

      <div class="tl-block">
        <h3 class="tl-head">教育经历</h3>
        <div class="tl">
          <div v-for="item in education" :key="item.period" class="tl-item">
            <div class="tl-line"></div>
            <div class="tl-dot"></div>
            <div class="tl-card">
              <div class="tl-period">{{ item.period }}</div>
              <div class="tl-school">{{ item.school }}<span class="tl-type">{{ item.type }}</span></div>
              <div class="tl-dept">{{ item.dept }}</div>
            </div>
          </div>
        </div>
      </div>

      <div class="tl-block">
        <h3 class="tl-head">工作经历</h3>
        <div class="tl">
          <div v-for="item in work" :key="item.period" class="tl-item">
            <div class="tl-line"></div>
            <div class="tl-dot"></div>
            <div class="tl-card">
              <div class="tl-period">{{ item.period }}</div>
              <div class="tl-school">{{ item.school }}<span class="tl-type">{{ item.role }}</span></div>
              <div class="tl-dept">{{ item.dept }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { education, work } from '../data/profile.js'
</script>

<style scoped>
.tl-block { margin-bottom: 30px; }
.tl-head {
  color: var(--accent);
  font-size: 16px;
  font-weight: 600;
  letter-spacing: 0.04em;
  margin: 0 0 16px;
}
.tl {
  position: relative;
  margin-left: 10px;
}
.tl-item {
  position: relative;
  padding-left: 28px;
  padding-bottom: 18px;
}
.tl-item:last-child { padding-bottom: 0; }
.tl-line {
  position: absolute;
  left: 3px;
  top: 10px;
  bottom: 0;
  width: 1px;
  background: var(--line-strong);
}
.tl-item:last-child .tl-line { display: none; }
.tl-dot {
  position: absolute;
  left: 0;
  top: 7px;
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: var(--accent);
}
.tl-card {
  background: var(--bg-soft);
  border: 1px solid var(--line);
  border-radius: 4px;
  padding: 14px 18px;
  transition: border-color 0.2s;
}
.tl-card:hover {
  border-color: var(--accent);
}
.tl-period {
  color: var(--accent);
  font-size: 14.5px;
  letter-spacing: 0.03em;
  margin-bottom: 5px;
}
.tl-school {
  color: var(--ink);
  font-size: 16.5px;
  font-weight: 600;
}
.tl-type {
  margin-left: 10px;
  font-size: 13px;
  font-weight: 400;
  color: var(--ink-soft);
  border: 1px solid var(--line-strong);
  border-radius: 999px;
  padding: 2px 10px;
  vertical-align: 1px;
}
.tl-dept {
  color: var(--ink-soft);
  font-size: 14.5px;
  margin-top: 4px;
}
</style>
