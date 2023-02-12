<template>
  <div class="flex items-center space-x-1 my-4">
    <div class="text-5xl md:text-9xl p-5 md:p-8 rounded-3xl bg-white/40 backdrop-blur-sm shadow-xl flex justify-center">
      <p class="relative">{{ hours }}</p>
      <p class="text-base md:text-xl font-semibold absolute bottom-2 md:bottom-5 leading-[1]">Jam</p>
    </div>
    <p class="text-5xl md:text-9xl">:</p>
    <div class="text-5xl md:text-9xl p-5 md:p-8 rounded-3xl bg-white/40 backdrop-blur-sm shadow-xl flex justify-center">
      <p class="relative">{{ minutes }}</p>
      <p class="text-base md:text-xl font-semibold absolute bottom-2 md:bottom-5 leading-[1]">Minit</p>
    </div>
    <p class="text-5xl md:text-9xl">:</p>
    <div class="text-5xl md:text-9xl p-5 md:p-8 rounded-3xl bg-white/40 backdrop-blur-sm shadow-xl flex justify-center">
      <p class="relative">{{ seconds }}</p>
      <p class="text-base md:text-xl font-semibold absolute bottom-2 md:bottom-5 leading-[1]">Saat</p>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { useNow } from '@vueuse/core'
import dayjs from 'dayjs'
import duration from 'dayjs/plugin/duration';

dayjs.extend(duration);

const props = defineProps({
  until: String,
})

const now = useNow()

const timeSpan = computed(() => {
  if (dayjs(props.until).isBefore(now.value)) {
    return dayjs.duration(0)
  } else {
    return dayjs.duration(dayjs(props.until).diff(now.value))
  }
})

const hours = computed(() => {
  const h = timeSpan.value.format('HH')
  return h
})

const minutes = computed(() => {
  const m = timeSpan.value.format('mm')
  return m
})

const seconds = computed(() => {
  const s = timeSpan.value.format('ss')
  return s
})
</script>