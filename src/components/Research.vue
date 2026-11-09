<template>
  <section id="research" class="section">
    <div class="section-inner">
      <h2 class="section-title"><span class="tick"></span>研究方向</h2>
      <div class="grid">
        <div v-for="(r, i) in research" :key="r" class="cell" :style="{ '--tile': tileColor(i) }">
          <div class="cell-bar"></div>
          <div class="cell-body">
            <div class="cell-name">{{ r }}</div>
            <div class="cell-num">0{{ i + 1 }}</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { research } from '../data/profile.js'

const colors = ['--tile1', '--tile2', '--tile3', '--tile4', '--tile5', '--tile6']
function tileColor(i) {
  return 'var(' + colors[i % colors.length] + ')'
}
</script>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
  gap: 16px;
}
.cell {
  position: relative;
  background: var(--bg-soft);
  border: 1px solid var(--line);
  border-radius: 6px;
  overflow: hidden;
  transition: border-color 0.2s, box-shadow 0.2s, transform 0.2s;
}
.cell:hover {
  border-color: var(--tile);
  box-shadow: 0 4px 16px rgba(56, 56, 56, 0.08);
  transform: translateY(-2px);
}
.cell-bar {
  height: 6px;
  background: var(--tile);
}
.cell-body {
  padding: 18px 20px 16px;
}
.cell-name {
  color: var(--ink);
  font-size: 16.5px;
  line-height: 1.6;
}
.cell-num {
  margin-top: 10px;
  font-family: var(--serif);
  font-size: 15px;
  font-weight: 600;
  color: var(--tile);
}
</style>
