<template>
  <section id="papers" class="section">
    <div class="section-inner">
      <h2 class="section-title"><span class="tick"></span>主要论文</h2>
      <p class="note">
        其中 # 表示共同一作，* 表示（共同）通讯。长期从事量子信息基础研究，累计发表论文 20 余篇，包括
        PNAS、Photonics Research、Physical Review Letters、Physical Review A 等期刊。
      </p>

      <div class="filter-bar">
        <button
          v-for="y in years"
          :key="y"
          :class="{ active: currentYear === y }"
          @click="setYear(y)"
        >{{ y }}</button>
      </div>

      <transition-group name="list" tag="div" class="paper-list">
        <div v-for="(p, i) in filtered" :key="p.title" class="paper" :class="{ highlight: p.highlight }">
          <div class="paper-meta">
            <span class="paper-year">{{ p.year }}</span>
            <span class="paper-journal">{{ p.journal }}</span>
          </div>
          <a
            :href="paperLink(p)"
            target="_blank"
            rel="noopener"
            class="paper-title"
          >{{ p.title }}</a>
          <div class="paper-authors">
            <template v-for="(part, pi) in authorParts(p)" :key="pi">
              <span :class="part.bold ? 'author-self' : ''">{{ part.text }}</span>
            </template>
          </div>
          <div class="paper-vol">
            <span>{{ p.vol }}</span>
            <span class="paper-doi">{{ p.doi }}</span>
          </div>
        </div>
      </transition-group>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'
import { papers } from '../data/profile.js'

const years = computed(() => [...new Set(papers.map((p) => p.year))].sort((a, b) => b - a))
const currentYear = ref('全部')

function setYear(y) {
  currentYear.value = y === currentYear.value ? '全部' : y
}

function paperLink(p) {
  if (p.doi && p.doi.startsWith('http')) return p.doi
  return 'https://doi.org/' + p.doi
}

const SELF = 'Xiaoqian Zhang'
const SELF_CN = '张晓倩'

function authorParts(p) {
  const text = p.authors || ''
  if (text.includes(SELF)) {
    const idx = text.indexOf(SELF)
    return [
      { text: text.slice(0, idx), bold: false },
      { text: SELF, bold: true },
      { text: text.slice(idx + SELF.length), bold: false },
    ]
  }
  if (text.includes(SELF_CN)) {
    const idx = text.indexOf(SELF_CN)
    return [
      { text: text.slice(0, idx), bold: false },
      { text: SELF_CN, bold: true },
      { text: text.slice(idx + SELF_CN.length), bold: false },
    ]
  }
  return [{ text, bold: false }]
}

const filtered = computed(() => {
  const list =
    currentYear.value === '全部'
      ? papers
      : papers.filter((p) => p.year === currentYear.value)
  return list
})
</script>

<style scoped>
.note {
  color: var(--ink-dim);
  font-size: 14.5px;
  line-height: 1.7;
  margin: 0 0 20px;
  max-width: 760px;
}
.filter-bar {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-bottom: 24px;
}
.filter-bar button {
  padding: 7px 15px;
  border: 1px solid var(--line-strong);
  background: var(--bg-soft);
  color: var(--ink-soft);
  font-size: 14px;
  cursor: pointer;
  transition: all 0.2s;
}
.filter-bar button:hover {
  border-color: var(--accent);
  color: var(--accent);
}
.filter-bar button.active {
  background: var(--accent);
  border-color: var(--accent);
  color: #fff;
}
.paper-list {
  display: flex;
  flex-direction: column;
  gap: 0;
}
.paper {
  position: relative;
  padding: 18px 20px;
  border-bottom: 1px solid var(--line);
  transition: background 0.2s;
}
.paper:hover {
  background: var(--accent-bg);
}
.paper.highlight {
  background: linear-gradient(to right, rgba(93, 169, 255, 0.08), transparent);
  border-left: 3px solid var(--accent);
  padding-left: 17px;
}
.paper-meta {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 8px;
}
.paper-year {
  font-family: var(--serif);
  font-weight: 600;
  color: var(--accent);
  font-size: 15px;
}
.paper-journal {
  color: var(--ink-dim);
  font-size: 13.5px;
  letter-spacing: 0.04em;
  text-transform: uppercase;
}
.paper-title {
  display: inline-block;
  color: var(--ink);
  font-size: 16.5px;
  font-weight: 500;
  line-height: 1.55;
  transition: color 0.15s;
}
.paper-title:hover {
  color: var(--accent);
  text-decoration: underline;
  text-underline-offset: 3px;
}
.paper-authors {
  color: var(--ink-soft);
  font-size: 14.5px;
  margin-top: 6px;
  line-height: 1.5;
}
.author-self {
  font-weight: 700;
  color: var(--ink);
  background: var(--accent-bg);
  padding: 0 3px;
  border-radius: 3px;
}
.paper-vol {
  color: var(--ink-dim);
  font-size: 13.5px;
  margin-top: 4px;
  font-style: italic;
  display: flex;
  align-items: center;
  gap: 10px;
}
.paper-doi {
  font-style: normal;
  color: var(--accent-blue);
  font-size: 12.5px;
  font-family: 'SFMono-Regular', Consolas, 'Liberation Mono', monospace;
  opacity: 0.85;
}
.list-enter-active, .list-leave-active {
  transition: all 0.2s ease;
}
.list-enter-from, .list-leave-to {
  opacity: 0;
  transform: translateY(6px);
}
</style>
