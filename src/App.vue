<template>
  <main class="bg-[url('/src/assets/bg-waktu-solat.webp')] bg-no-repeat bg-cover bg-center">
    <div v-if="error" class="container mx-auto">
      <div class="flex flex-col items-center justify-center h-screen">
        <h1 class="text-red-700 text-lg">Error: {{ error }}</h1>
      </div>
    </div>
    <div v-else-if="isFetching" class="container mx-auto">
      <div class="flex flex-col items-center justify-center h-screen">
        <div class="flex items-center justify-center space-x-2">
          <div class="w-8 h-8 rounded-full animate-pulse bg-gray-500"></div>
          <div class="w-8 h-8 rounded-full animate-pulse bg-gray-500"></div>
          <div class="w-8 h-8 rounded-full animate-pulse bg-gray-500"></div>
          <div class="w-8 h-8 rounded-full animate-pulse bg-gray-500"></div>
        </div>
      </div>
    </div>
    <div v-else class="container mx-auto">
      <div class="flex flex-col items-center justify-center h-[calc(100vh-36px)] min-h-[736px] mb-3">
        <h1 class="text-xl md:text-4xl font-bold text-center mx-1 md:mx-0">{{ miladiDate }} Miladi | {{ hijriDate }}
          Hijri
        </h1>
        <h2 class="text-lg md:text-2xl font-semibold">Waktu Solat Seterusnya</h2>
        <h3 class="text-5xl md:text-8xl font-semibold -mt-2">{{ currentPrayerName }}</h3>
        <h4 class="text-xl md:text-3xl font-semibold">{{ currentPrayerTime }}</h4>
        <Countdown :until="until" />
        <Zone v-model="state.zone" :bearing="defaultBearing" />
        <Schedule :prayer="prayer" :tomorrow="tomorrow" />
        <Azan :open="open" @click-event="setOpenTrue" />
      </div>
    </div>
    <Footer />
  </main>
</template>

<script setup>
import { useFetch, useNow, useStorage } from '@vueuse/core'
import { ref, watch } from 'vue'
import Countdown from './components/Countdown.vue'
import Zone from './components/Zone.vue'
import Schedule from './components/Schedule.vue'
import Azan from './components/Azan.vue'
import Footer from './components/Footer.vue'
import dayjs from 'dayjs'
import 'dayjs/locale/ms'

const open = ref(false)
const tomorrow = ref(false)

const setOpenTrue = () => {
  open.value = !open.value
};

const hijriMonths = ["Muharram", "Safar", "Rabiul Awal", "Rabiul Akhir", "Jamadil Awal", "Jamadil Akhir", "Rejab",
  "Syaaban", "Ramadan", "Syawal", "Zulkaedah", "Zulhijjah"]

let currentDate = dayjs().format('DD MMMM YYYY')
const miladiDate = ref(currentDate)
const hijriDate = ref('Loading...')

const now = useNow()
const prayer = ref({
  asr: "00:00:00",
  dhuhr: "00:00:00",
  fajr: "00:00:00",
  imsak: "00:00:00",
  isha: "00:00:00",
  maghrib: "00:00:00",
  syuruk: "00:00:00"
})

const until = ref(currentDate)
const currentPrayerName = ref('')
const currentPrayerTime = ref('')

watch(now, (now) => {
  let nowDate = currentDate

  if (tomorrow.value) {
    nowDate = dayjs().add(1, 'day').format('DD MMMM YYYY')
  }

  if (dayjs(now.value).isBefore(dayjs(nowDate + ' ' + prayer.value.fajr))) {
    until.value = dayjs(nowDate + ' ' + prayer.value.fajr).format()
    currentPrayerName.value = 'Subuh'
    currentPrayerTime.value = dayjs(nowDate + ' ' + prayer.value.fajr).format('hh:mm A')
  } else if (dayjs(now.value).isBefore(dayjs(nowDate + ' ' + prayer.value.dhuhr))) {
    until.value = dayjs(nowDate + ' ' + prayer.value.dhuhr).format()
    currentPrayerName.value = 'Zohor'
    currentPrayerTime.value = dayjs(nowDate + ' ' + prayer.value.dhuhr).format('hh:mm A')
  } else if (dayjs(now.value).isBefore(dayjs(nowDate + ' ' + prayer.value.asr))) {
    until.value = dayjs(nowDate + ' ' + prayer.value.asr).format()
    currentPrayerName.value = 'Asar'
    currentPrayerTime.value = dayjs(nowDate + ' ' + prayer.value.asr).format('hh:mm A')
  } else if (dayjs(now.value).isBefore(dayjs(nowDate + ' ' + prayer.value.maghrib))) {
    until.value = dayjs(nowDate + ' ' + prayer.value.maghrib).format()
    currentPrayerName.value = 'Maghrib'
    currentPrayerTime.value = dayjs(nowDate + ' ' + prayer.value.maghrib).format('hh:mm A')
  } else if (dayjs(now.value).isBefore(dayjs(nowDate + ' ' + prayer.value.isha))) {
    until.value = dayjs(nowDate + ' ' + prayer.value.isha).format()
    currentPrayerName.value = 'Isyak'
    currentPrayerTime.value = dayjs(nowDate + ' ' + prayer.value.isha).format('hh:mm A')
  }

  if (dayjs(now.value).isSame(dayjs(nowDate + ' ' + prayer.value.fajr), 'minute')) {
    open.value = true
  } else if (dayjs(now.value).isSame(dayjs(nowDate + ' ' + prayer.value.dhuhr), 'minute')) {
    open.value = true
  } else if (dayjs(now.value).isSame(dayjs(nowDate + ' ' + prayer.value.asr), 'minute')) {
    open.value = true
  } else if (dayjs(now.value).isSame(dayjs(nowDate + ' ' + prayer.value.maghrib), 'minute')) {
    open.value = true
  } else if (dayjs(now.value).isSame(dayjs(nowDate + ' ' + prayer.value.isha), 'minute')) {
    open.value = true
  }
})

const defaultSelect = {
  zone: 'WLY01'
}
const defaultBearing = ref('(' + '292&#176; 20&#8242; 35&#8243;' + ')')

const state = useStorage('zone-storage', defaultSelect)

const url = ref('https://www.e-solat.gov.my/index.php?r=esolatApi/TakwimSolat&period=today&zone=' + state.value.zone)

watch(state, (state) => {
  url.value = 'https://www.e-solat.gov.my/index.php?r=esolatApi/TakwimSolat&period=today&zone=' + state.zone
})

const { isFetching, error, data, onFetchResponse } = useFetch(url, { refetch: true }).json()

onFetchResponse(() => {
  if (dayjs(now.value).isAfter(dayjs(dayjs().format('DD MMMM YYYY') + ' ' + data.value.prayerTime[0].isha))) {
    url.value = 'https://www.e-solat.gov.my/index.php?r=esolatApi/takwimsolat&period=date&zone=' + state.value.zone + '&date=' + dayjs().add(1, 'day').format('YYYY-MM-DD')
    tomorrow.value = true
  }

  miladiDate.value = dayjs(data.value.prayerTime[0].date).locale('ms').format('DD MMMM YYYY')

  const hijriArray = data.value.prayerTime[0].hijri.split('-')
  hijriDate.value = hijriArray[2] + ' ' + hijriMonths[parseInt(hijriArray[1]) - 1] + ' ' + hijriArray[0]
  prayer.value.asr = data.value.prayerTime[0].asr
  prayer.value.dhuhr = data.value.prayerTime[0].dhuhr
  prayer.value.fajr = data.value.prayerTime[0].fajr
  prayer.value.imsak = data.value.prayerTime[0].imsak
  prayer.value.isha = data.value.prayerTime[0].isha
  prayer.value.maghrib = data.value.prayerTime[0].maghrib
  prayer.value.syuruk = data.value.prayerTime[0].syuruk

  defaultBearing.value = data.value.bearing !== undefined ? '(' + data.value.bearing + ')' : ''
})
</script>
