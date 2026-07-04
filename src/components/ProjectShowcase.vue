<script setup>
import { computed, ref } from 'vue'
import catalog from '@/data/projects.json'

const meta = catalog.meta
const allProjects = catalog.projects

const activeCategory = ref('all')
const activeStatus = ref('all')

const categories = computed(() => {
  const present = new Set(allProjects.map((p) => p.category))
  return ['all', ...meta.categories.filter((c) => present.has(c))]
})

const statuses = computed(() => {
  const present = new Set(allProjects.map((p) => p.status))
  return ['all', ...meta.statuses.filter((s) => present.has(s))]
})

const filteredProjects = computed(() =>
  allProjects.filter((p) => {
    const okCategory = activeCategory.value === 'all' || p.category === activeCategory.value
    const okStatus = activeStatus.value === 'all' || p.status === activeStatus.value
    return okCategory && okStatus
  }),
)

function setCategory(category) {
  activeCategory.value = category
}

function setStatus(status) {
  activeStatus.value = status
}

function statusClass(status) {
  return `status-${status.toLowerCase()}`
}
</script>

<template>
  <section class="showcase">
    <header class="showcase-head">
      <h2>{{ meta.org }}</h2>
      <p class="showcase-lead">{{ meta.description }}</p>
    </header>

    <div class="showcase-filters">
      <fieldset class="filter-group">
        <legend>Kategoria</legend>
        <button
          v-for="category in categories"
          :key="category"
          type="button"
          class="filter-chip"
          :class="{ 'is-active': activeCategory === category }"
          @click="setCategory(category)"
        >
          {{ category === 'all' ? 'wszystkie' : category }}
        </button>
      </fieldset>

      <fieldset class="filter-group">
        <legend>Status</legend>
        <button
          v-for="status in statuses"
          :key="status"
          type="button"
          class="filter-chip"
          :class="{ 'is-active': activeStatus === status }"
          @click="setStatus(status)"
        >
          {{ status === 'all' ? 'wszystkie' : status }}
        </button>
      </fieldset>
    </div>

    <p class="showcase-count">
      {{ filteredProjects.length }} / {{ allProjects.length }} projektów
    </p>

    <ul class="showcase-grid">
      <li v-for="project in filteredProjects" :key="project.name" class="project-card">
        <div class="project-card-top">
          <span class="project-category">{{ project.category }}</span>
          <span class="project-status" :class="statusClass(project.status)">{{
            project.status
          }}</span>
        </div>
        <h3 class="project-name">
          <a :href="project.url" target="_blank" rel="noopener noreferrer">{{ project.name }}</a>
        </h3>
        <p class="project-description">{{ project.description }}</p>
        <div class="project-card-bottom">
          <span v-if="project.language" class="project-language">{{ project.language }}</span>
          <span v-if="project.fork" class="project-forkflag">fork</span>
        </div>
      </li>
    </ul>

    <p v-if="filteredProjects.length === 0" class="showcase-empty">
      Brak projektów dla wybranych filtrów.
    </p>

    <footer class="showcase-foot">
      <a :href="meta.declaration" target="_blank" rel="noopener noreferrer"
        >Universal Independency Declaration</a
      >
      ·
      <a :href="meta.orgUrl" target="_blank" rel="noopener noreferrer">github.com/ipicoin</a>
    </footer>
  </section>
</template>

<style scoped>
.showcase {
  max-width: 1100px;
  margin: 0 auto;
  padding: 2rem 1rem;
}

.showcase-head h2 {
  font-size: 1.6rem;
  font-weight: 700;
  margin-bottom: 0.4rem;
}

.showcase-lead {
  opacity: 0.8;
  max-width: 70ch;
}

.showcase-filters {
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
  margin: 1.5rem 0 0.5rem;
}

.filter-group {
  border: none;
  padding: 0;
  margin: 0;
}

.filter-group legend {
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  opacity: 0.6;
  margin-bottom: 0.4rem;
}

.filter-chip {
  cursor: pointer;
  border: 1px solid currentColor;
  background: transparent;
  color: inherit;
  border-radius: 999px;
  padding: 0.25rem 0.75rem;
  margin: 0 0.35rem 0.35rem 0;
  font-size: 0.8rem;
  opacity: 0.65;
  transition: opacity 0.15s ease, background 0.15s ease;
}

.filter-chip:hover {
  opacity: 1;
}

.filter-chip.is-active {
  opacity: 1;
  background: #2563eb;
  color: #fff;
  border-color: #2563eb;
}

.showcase-count {
  font-size: 0.8rem;
  opacity: 0.6;
  margin: 0.5rem 0 1rem;
}

.showcase-grid {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 1rem;
}

.project-card {
  border: 1px solid rgba(127, 127, 127, 0.3);
  border-radius: 10px;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  min-height: 100%;
  transition: border-color 0.15s ease, transform 0.15s ease;
}

.project-card:hover {
  border-color: rgba(127, 127, 127, 0.7);
  transform: translateY(-2px);
}

.project-card-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 0.5rem;
}

.project-category {
  font-size: 0.7rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  opacity: 0.6;
}

.project-status {
  font-size: 0.68rem;
  font-weight: 700;
  padding: 0.1rem 0.45rem;
  border-radius: 999px;
  border: 1px solid currentColor;
  white-space: nowrap;
}

.status-pre-alpha {
  color: #c47f00;
}

.status-early-dev {
  color: #2b7de9;
}

.status-stable {
  color: #1f9d55;
}

.status-fork {
  color: #8a63d2;
}

.project-name {
  font-size: 1.05rem;
  font-weight: 700;
  margin: 0 0 0.4rem;
  word-break: break-word;
}

.project-name a {
  color: inherit;
  text-decoration: none;
}

.project-name a:hover {
  text-decoration: underline;
}

.project-description {
  font-size: 0.85rem;
  line-height: 1.4;
  opacity: 0.85;
  flex: 1 1 auto;
  margin: 0 0 0.75rem;
}

.project-card-bottom {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.72rem;
  opacity: 0.7;
}

.project-language::before {
  content: '●';
  margin-right: 0.3rem;
}

.project-forkflag {
  border: 1px solid currentColor;
  border-radius: 4px;
  padding: 0 0.35rem;
}

.showcase-empty {
  opacity: 0.6;
  padding: 2rem 0;
  text-align: center;
}

.showcase-foot {
  margin-top: 2rem;
  font-size: 0.8rem;
  opacity: 0.7;
}

.showcase-foot a {
  color: inherit;
}
</style>
