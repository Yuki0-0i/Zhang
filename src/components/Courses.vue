<template>
  <section id="courses" class="section">
    <div class="section-inner">
      <h2 class="section-title"><span class="tick"></span>讲授课程</h2>
      <div class="course-grid">
        <div
          v-for="(c, i) in courses"
          :key="c.name"
          class="course"
          :style="{ '--tile': tileColor(i) }"
        >
          <div class="course-bar"></div>
          <div class="course-body">
            <div class="course-name">{{ c.name }}</div>
            <div class="course-level">{{ c.level }}</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { courses } from '../data/profile.js'

const colors = ['--tile1', '--tile2', '--tile3', '--tile4', '--tile5', '--tile6']
function tileColor(i) {
  return 'var(' + colors[i % colors.length] + ')'
}
</script>

<style scoped>
.course-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 16px;
}
.course {
  background: var(--bg-soft);
  border: 1px solid var(--line);
  border-radius: 6px;
  overflow: hidden;
  transition: border-color 0.2s, box-shadow 0.2s, transform 0.2s;
}
.course:hover {
  border-color: var(--tile);
  box-shadow: 0 4px 16px rgba(56, 56, 56, 0.08);
  transform: translateY(-2px);
}
.course-bar {
  height: 6px;
  background: var(--tile);
}
.course-body {
  padding: 18px;
}
.course-name {
  color: var(--ink);
  font-size: 16.5px;
  font-weight: 500;
  line-height: 1.5;
}
.course-level {
  color: var(--ink-dim);
  font-size: 14px;
  margin-top: 6px;
}
</style>
