<template>
  <section id="about" class="section">
    <div class="section-inner">
      <h2 class="section-title"><span class="tick"></span>个人简介</h2>
      <div class="about-grid">
        <div class="card about-card">
          <ul class="facts">
            <li><span class="k">姓名</span><span class="v">{{ profile.name }}</span></li>
            <li><span class="k">职称</span><span class="v">{{ profile.title }}</span></li>
            <li><span class="k">学位</span><span class="v">博士</span></li>
            <li><span class="k">部门</span><span class="v">{{ profile.affiliation }}</span></li>
            <li><span class="k">邮箱</span><span class="v">{{ profile.email }}</span></li>
            <li><span class="k">地址</span><span class="v">{{ profile.location }}</span></li>
          </ul>
        </div>
        <div class="card intro-card">
          <p v-for="(t, i) in profile.intro" :key="i" class="intro-text">{{ t }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { profile } from '../data/profile.js'
</script>

<style scoped>
.about-grid {
  display: grid;
  grid-template-columns: 300px 1fr;
  gap: 20px;
}
.card {
  background: var(--bg-soft);
  border: 1px solid var(--line);
  border-radius: 4px;
  padding: 24px;
}
.facts {
  list-style: none;
  margin: 0;
  padding: 0;
}
.facts li {
  display: flex;
  gap: 12px;
  padding: 8px 0;
  border-bottom: 1px solid var(--line);
  font-size: 15.5px;
}
.facts li:last-child { border-bottom: none; }
.k {
  flex-shrink: 0;
  color: var(--ink-dim);
  width: 48px;
}
.v {
  color: var(--ink-soft);
  word-break: break-all;
}
.intro-text {
  color: var(--ink-soft);
  line-height: 2;
  font-size: 16.5px;
  margin: 0 0 14px;
}
.intro-text:last-child { margin-bottom: 0; }
@media (max-width: 800px) {
  .about-grid { grid-template-columns: 1fr; }
}
</style>
