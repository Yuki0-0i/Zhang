<template>
  <div class="site">
    <header class="nav">
      <div class="nav-inner">
        <div class="nav-brand">张晓倩 <span class="brand-en">· Xiaoqian Zhang</span></div>
        <nav class="nav-links">
          <a
            v-for="item in navItems"
            :key="item.id"
            :href="'#' + item.id"
            class="nav-link"
            :class="{ active: activeId === item.id }"
            @click.prevent="goTo(item.id)"
          >
            <svg class="nav-icon" viewBox="0 0 24 24" aria-hidden="true">
              <path v-html="item.icon" />
            </svg>
            <span>{{ item.label }}</span>
          </a>
        </nav>
      </div>
    </header>

    <main>
      <Hero />
      <About />
      <Timeline />
      <Research />
      <Publications />
      <Projects />
      <Courses />
    </main>

    <footer class="footer">
      <div class="footer-inner">
        <p>张晓倩 · 暨南大学 信息科学技术学院 计算机科学系</p>
        <p class="footer-meta">个人学术主页 · 量子信息与量子计算</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Timeline from './components/Timeline.vue'
import Research from './components/Research.vue'
import Publications from './components/Publications.vue'
import Projects from './components/Projects.vue'
import Courses from './components/Courses.vue'

const navItems = [
  {
    id: 'about',
    label: '个人简介',
    icon: '<path d="M12 12c2.5 0 4.5-2 4.5-4.5S14.5 3 12 3S7.5 5 7.5 7.5S9.5 12 12 12zm0 2c-3 0-7 1.6-7 4.2V19h14v-0.8c0-2.6-4-4.2-7-4.2z"/>',
  },
  {
    id: 'timeline',
    label: '经历',
    icon: '<path d="M4 5h16v2H4V5zm0 5h16v2H4v-2zm0 5h10v2H4v-2zm13 0l3 3l-3 3v-2h-3v-2h3v-2z"/>',
  },
  {
    id: 'research',
    label: '研究方向',
    icon: '<path d="M12 4a8 8 0 1 1 0 16a8 8 0 0 1 0-16zm0 2a6 6 0 1 0 0 12a6 6 0 0 0 0-12zm3.5 2l-1.7 3.4l-3.3 1.6l3.3 1.6l1.7 3.4l1.7-3.4L19 12l-3.3-1.6L15.5 8z"/>',
  },
  {
    id: 'papers',
    label: '论文',
    icon: '<path d="M6 3h9l5 5v13a1 1 0 0 1-1 1H6a1 1 0 0 1-1-1V4a1 1 0 0 1 1-1zm9 1.5L18.5 8H15V4.5zM7 12h10v2H7v-2zm0 3h7v2H7v-2z"/>',
  },
  {
    id: 'projects',
    label: '课题',
    icon: '<path d="M12 3l8 4v6c0 4-3.4 7.3-8 8c-4.6-0.7-8-4-8-8V7l8-4zm0 2.2L6 8.3v4.7c0 3 2.2 5.4 6 6.1c3.8-0.7 6-3.1 6-6.1V8.3l-6-3.1zm-1 3h2v2h2v2h-2v2h-2v-2H9v-2h2V8.2z"/>',
  },
  {
    id: 'courses',
    label: '课程',
    icon: '<path d="M4 5c0-1.1 0.9-2 2-2h13v16H6a2 2 0 0 0-2 2V5zm2 0v11h11V5H6zm2 2h6v1H8V7zm0 2h6v1H8V9zm0 2h6v1H8v-1zm7 4v1h2v-1h-2z"/>',
  },
]

const activeId = ref('')
let scrollTimer = null

function goTo(id) {
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}

function onScroll() {
  clearTimeout(scrollTimer)
  scrollTimer = setTimeout(() => {
    const offsets = navItems.map((item) => ({
      id: item.id,
      top: document.getElementById(item.id)?.offsetTop ?? 0,
    }))
    const pos = window.scrollY + 90
    let current = ''
    for (const o of offsets) {
      if (pos >= o.top) current = o.id
    }
    activeId.value = current
  }, 60)
}

onMounted(() => {
  onScroll()
  window.addEventListener('scroll', onScroll, { passive: true })
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', onScroll)
  clearTimeout(scrollTimer)
})
</script>

<style scoped>
.site {
  position: relative;
  min-height: 100vh;
  background:
    radial-gradient(900px 500px at 15% -10%, rgba(93, 169, 255, 0.12), transparent 60%),
    radial-gradient(1000px 600px at 90% 5%, rgba(124, 58, 237, 0.08), transparent 55%),
    linear-gradient(to bottom, rgba(255, 255, 255, 0.3), rgba(242, 246, 255, 0.92)),
    repeating-linear-gradient(0deg, transparent 0 23px, rgba(56, 56, 56, 0.02) 23px 24px),
    repeating-linear-gradient(90deg, transparent 0 23px, rgba(56, 56, 56, 0.02) 23px 24px);
}
.nav {
  position: sticky;
  top: 0;
  z-index: 50;
  background: rgba(255, 255, 255, 0.92);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--line);
}
.nav-inner {
  max-width: 1060px;
  margin: 0 auto;
  padding: 16px 24px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.nav-brand {
  font-family: var(--serif);
  font-weight: 600;
  font-size: 17px;
  color: var(--ink);
}
.brand-en {
  font-size: 13px;
  color: var(--ink-dim);
  font-weight: 400;
}
.nav-links {
  display: flex;
  gap: 6px;
}
.nav-link {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
  padding: 7px 16px;
  border-radius: 999px;
  border: none;
  color: #fff;
  font-size: 15px;
  line-height: 1;
  background: linear-gradient(135deg, var(--accent) 0%, var(--accent-blue) 100%);
  box-shadow: 0 3px 10px rgba(93, 169, 255, 0.3);
  transition: all 0.2s;
}
.nav-icon {
  display: block;
  width: 15px;
  height: 15px;
  fill: currentColor;
  flex-shrink: 0;
}
.nav-link:hover {
  background: linear-gradient(135deg, var(--accent-strong) 0%, var(--accent-blue-strong) 100%);
  box-shadow: 0 5px 14px rgba(93, 169, 255, 0.42);
  transform: translateY(-1px);
}
.nav-link.active {
  background: linear-gradient(135deg, var(--accent-strong) 0%, var(--accent-blue-strong) 100%);
  box-shadow: 0 4px 14px rgba(93, 169, 255, 0.5);
}
.footer {
  border-top: 1px solid var(--line);
  margin-top: 48px;
  background: var(--bg-soft);
}
.footer-inner {
  max-width: 1060px;
  margin: 0 auto;
  padding: 26px 24px;
  text-align: center;
  color: var(--ink-dim);
  font-size: 14px;
}
.footer-meta {
  margin-top: 4px;
}
@media (max-width: 640px) {
  .nav-inner {
    flex-direction: column;
    gap: 10px;
    padding: 12px 16px;
  }
  .nav-links {
    gap: 6px;
    flex-wrap: wrap;
    justify-content: center;
  }
}
</style>
