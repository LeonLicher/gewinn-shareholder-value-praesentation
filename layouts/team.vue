<script setup>
import SlideLayout from '@components/SlideLayout.vue'

const info = $slidev.configs?.presentationInfo || { authors: [] }

const initials = name =>
  name
    .trim()
    .split(/\s+/)
    .map(part => part[0])
    .join('')
    .toLocaleUpperCase('de-DE')
</script>

<template>
  <SlideLayout title="Vorstellung">
    <div class="flex-1 flex items-center justify-center">
      <div class="team-grid" role="list" aria-label="Mitglieder der Gruppe 1">
        <div v-for="author in info.authors" :key="author.name" class="team-card" role="listitem">
          <span class="team-initials" aria-hidden="true">{{ initials(author.name) }}</span>
          <p class="team-name">{{ author.name }}</p>
        </div>
      </div>
    </div>
  </SlideLayout>
</template>

<style scoped>
.team-grid {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 2rem 1.5rem;
  width: 100%;
  max-width: 38rem;
}

.team-card {
  grid-column: span 2;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  text-align: center;
}

.team-card:nth-child(4) {
  grid-column: 2 / span 2;
}

.team-initials {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 5rem;
  height: 5rem;
  border-radius: 0.6rem;
  background: #0066b3;
  color: white;
  font-size: 2rem;
  font-weight: 800;
  line-height: 1;
  letter-spacing: 0.02em;
}

.team-name {
  margin: 0;
  color: #10245e;
  font-size: 1rem;
  font-weight: 600;
  line-height: 1.3;
}
</style>
