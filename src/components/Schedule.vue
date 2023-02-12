<template>
  <div class="w-full md:w-auto ">
    <div class="rounded-xl bg-white/40 backdrop-blur-sm shadow-lg mx-3 md:mx-0 mt-6 py-4 px-5">
      <h4 class="text-center mb-4 font-extrabold text-xl">Jadual Waktu Solat Hari Ini</h4>
      <div class="grid grid-cols-3 md:grid-cols-7 gap-6">
        <div class="flex flex-col justify-center items-center">
          <p class="font-bold text-base">Imsak</p>
          <p>{{ prayerDayjs.imsak }}</p>
        </div>
        <div class="flex flex-col justify-center items-center">
          <p class="font-bold text-base">Subuh</p>
          <p>{{ prayerDayjs.fajr }}</p>
        </div>
        <div class="flex flex-col justify-center items-center">
          <p class="font-bold text-base">Syuruk</p>
          <p>{{ prayerDayjs.syuruk }}</p>
        </div>
        <div class="flex flex-col justify-center items-center">
          <p class="font-bold text-base">Zohor</p>
          <p>{{ prayerDayjs.dhuhr }}</p>
        </div>
        <div class="flex flex-col justify-center items-center">
          <p class="font-bold text-base">Asar</p>
          <p>{{ prayerDayjs.asr }}</p>
        </div>
        <div class="flex flex-col justify-center items-center">
          <p class="font-bold text-base">Maghrib</p>
          <p>{{ prayerDayjs.maghrib }}</p>
        </div>
        <div class="flex flex-col justify-center items-center">
          <p class="font-bold text-base">Isyak</p>
          <p>{{ prayerDayjs.isha }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import dayjs from 'dayjs'
import { computed } from 'vue';

const props = defineProps({
  prayer: Object,
  tomorrow: Boolean
})

const prayerDayjs = computed(() => {
  let currentDate = dayjs().format('DD MMMM YYYY')
  if (props.tomorrow) {
    currentDate = dayjs().add(1, 'day').format('DD MMMM YYYY')
  }

  return {
    asr: dayjs(currentDate + ' ' + props.prayer.asr).format('hh:mm A'),
    dhuhr: dayjs(currentDate + ' ' + props.prayer.dhuhr).format('hh:mm A'),
    fajr: dayjs(currentDate + ' ' + props.prayer.fajr).format('hh:mm A'),
    imsak: dayjs(currentDate + ' ' + props.prayer.imsak).format('hh:mm A'),
    isha: dayjs(currentDate + ' ' + props.prayer.isha).format('hh:mm A'),
    maghrib: dayjs(currentDate + ' ' + props.prayer.maghrib).format('hh:mm A'),
    syuruk: dayjs(currentDate + ' ' + props.prayer.syuruk).format('hh:mm A'),
  }
})
</script>