<script setup>
defineProps({
  authors: {
    type: Array,
    default: () => []
  }
})
</script>

<template>
  <div
    v-if="authors?.length"
    :class="['grid gap-x-6', authors.length > 2 ? 'grid-cols-3 gap-y-2' : 'grid-cols-2 gap-y-6']"
  >
    <div v-for="author in authors" :key="author.name" class="flex items-center gap-3">
      <img
        v-if="author.image"
        :src="author.image"
        :alt="author.name"
        class="h-14 w-14 rounded-full object-cover object-top border border-gray-200"
      />
      <div>
        <p class="text-base font-semibold text-gray-800 mb-0.5">{{ author.name }}</p>
        <p
          v-if="author.matrikelnummer || author.email"
          class="text-xs text-gray-600 leading-relaxed"
        >
          <template v-if="author.matrikelnummer"
            >Matrikelnummer: {{ author.matrikelnummer }}<br
          /></template>
          {{ author.email }}
        </p>
      </div>
    </div>
  </div>
</template>
