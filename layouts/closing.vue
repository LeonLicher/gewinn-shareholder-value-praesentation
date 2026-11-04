<script setup>
import CoverBackdrop from '@components/CoverBackdrop.vue'
import CoverLogo from '@layouts/CoverLogo.vue'
</script>

<template>
  <div class="slide-padding-x h-full bg-white relative overflow-hidden flex flex-col pt-12 pb-14">
    <CoverBackdrop variant="closing" />

    <div class="relative z-10 flex flex-col h-full">
      <CoverLogo />

      <div class="flex-1 flex flex-col justify-center -mt-8">
        <h1 class="text-[5.5rem] leading-[0.95] font-black text-fh-navy tracking-tight mb-5">
          Vielen Dank
        </h1>
        <p class="text-3xl text-fh-orange font-normal">Gibt es noch Fragen?</p>
      </div>

      <div class="h-px w-full bg-fh-line" />
    </div>
  </div>
</template>
