<template>
  <section class="hero">
    <div class="hero-inner">
      <div class="avatar">
        <span class="av-text">XQ</span>
      </div>
      <h1 class="name">{{ profile.name }}</h1>
      <div class="name-en">{{ profile.nameEn }}</div>
      <div class="title">{{ profile.title }}</div>
      <div class="affil">{{ profile.affiliation }}</div>
      <div class="tags">
        <span v-for="t in profile.tags" :key="t" class="tag">{{ t }}</span>
      </div>
      <div class="cta">
        <a href="#papers" class="btn primary">代表性论文</a>
        <a href="#about" class="btn ghost">个人简介</a>
      </div>
    </div>
  </section>
</template>

<script setup>
import { profile } from '../data/profile.js'
</script>

<style scoped>
.hero {
  min-height: 82vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 64px 24px 40px;
}
.avatar {
  width: 92px;
  height: 92px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 26px;
  font-weight: 600;
  letter-spacing: 0.05em;
  color: var(--accent);
  background: var(--accent-bg);
  border: 1px solid var(--accent);
  margin: 0 auto 24px;
}
.name {
  font-family: var(--serif);
  font-size: clamp(40px, 6vw, 56px);
  font-weight: 600;
  letter-spacing: 0.04em;
  margin: 0;
  background: linear-gradient(135deg, var(--accent) 0%, var(--accent-blue) 100%);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
}
.name-en {
  margin-top: 6px;
  font-size: 17px;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: var(--ink-dim);
}
.title {
  margin-top: 18px;
  font-size: 19px;
  color: var(--ink-soft);
}
.affil {
  margin-top: 6px;
  font-size: 16px;
  color: var(--ink-dim);
}
.tags {
  margin-top: 22px;
  display: flex;
  gap: 8px;
  justify-content: center;
  flex-wrap: wrap;
}
.tag {
  padding: 5px 14px;
  border: 1px solid var(--line-strong);
  color: var(--ink-soft);
  font-size: 15px;
  background: var(--bg-soft);
}
.cta {
  margin-top: 30px;
  display: flex;
  gap: 12px;
  justify-content: center;
  flex-wrap: wrap;
}
.btn {
  padding: 10px 24px;
  text-decoration: none;
  font-size: 14px;
  transition: all 0.2s;
}
.btn.primary {
  background: linear-gradient(135deg, var(--accent), var(--accent-blue));
  color: #fff;
  box-shadow: 0 4px 14px rgba(93, 169, 255, 0.3);
}
.btn.primary:hover {
  background: linear-gradient(135deg, var(--accent-strong), var(--accent-blue-strong));
  transform: translateY(-1px);
}
.btn.ghost {
  border: 1px solid var(--line-strong);
  color: var(--ink-soft);
}
.btn.ghost:hover {
  border-color: var(--accent);
  color: var(--accent);
}
</style>
