<script setup>
defineProps({
  department: {
    type: Boolean,
    default: true
  }
})
</script>

<template>
  <div class="flex items-center gap-7">
    <img src="/images/fh-logo.jpg" alt="FH Münster" class="h-16" />

    <template v-if="department">
      <div class="h-12 w-px bg-fh-line" />
      <img src="/images/msb.png" alt="FB Wirtschaft – Münster School of Business" class="h-16" />
    </template>
  </div>
</template>
