<template>
  <h4 class="text-lg md:text-2xl font-semibold text-center">Sehingga Waktu Solat
    Seterusnya Di Zon</h4>
  <h4 class="font-bold text-base md:text-2xl text-center">{{ zoneName }}
    <span v-html="bearing"></span>
  </h4>
  <div class="w-full md:w-[520px] px-3 md:px-0 mt-3">
    <select :value="modelValue" @input="$emit('update:modelValue', $event.target.value)"
      class="block w-full mt-1 rounded-lg bg-white/40 backdrop-blur-sm border-gray-300 shadow-lg border-transparent focus:border-transparent focus:ring-0">
      <optgroup label="Johor">
        <option value="JHR01">Pulau Aur dan Pulau Pemanggil </option>
        <option value="JHR02">Johor Bahru, Kota Tinggi, Mersing, Kulai</option>
        <option value="JHR03">Kluang, Pontian</option>
        <option value="JHR04">Batu Pahat, Muar, Segamat, Gemas Johor, Tangkak</option>
      </optgroup>
      <optgroup label="Kedah">
        <option value="KDH01">Kota Setar, Kubang Pasu, Pokok Sena (Daerah Kecil)</option>
        <option value="KDH02">Kuala Muda, Yan, Pendang</option>
        <option value="KDH03">Padang Terap, Sik</option>
        <option value="KDH04">Baling</option>
        <option value="KDH05">Bandar Baharu, Kulim</option>
        <option value="KDH06">Langkawi</option>
        <option value="KDH07">Puncak Gunung Jerai</option>
      </optgroup>
      <optgroup label="Kelantan">
        <option value="KTN01">Bachok, Kota Bharu, Machang, Pasir Mas, Pasir Puteh, Tanah Merah, Tumpat, Kuala Krai,
          Mukim Chiku</option>
        <option value="KTN02">Gua Musang (Daerah Galas Dan Bertam), Jeli, Jajahan Kecil Lojing</option>
      </optgroup>
      <optgroup label="Melaka">
        <option value="MLK01">Seluruh Negeri Melaka</option>
      </optgroup>
      <optgroup label="Negeri Sembilan">
        <option value="NGS01">Tampin, Jempol</option>
        <option value="NGS02">Jelebu, Kuala Pilah, Rembau</option>
        <option value="NGS03">Port Dickson, Seremban</option>
      </optgroup>
      <optgroup label="Pahang">
        <option value="PHG01">Pulau Tioman</option>
        <option value="PHG02">Kuantan, Pekan, Rompin, Muadzam Shah</option>
        <option value="PHG03">Jerantut, Temerloh, Maran, Bera, Chenor, Jengka</option>
        <option value="PHG04">Bentong, Lipis, Raub</option>
        <option value="PHG05">Genting Sempah, Janda Baik, Bukit Tinggi</option>
        <option value="PHG06">Cameron Highlands, Genting Higlands, Bukit Fraser</option>
      </optgroup>
      <optgroup label="Perlis">
        <option value="PLS01">Kangar, Padang Besar, Arau</option>
      </optgroup>
      <optgroup label="Pulau Pinang">
        <option value="PNG01">Seluruh Negeri Pulau Pinang</option>
      </optgroup>
      <optgroup label="Perak">
        <option value="PRK01">Tapah, Slim River, Tanjung Malim</option>
        <option value="PRK02">Kuala Kangsar, Sg. Siput, Ipoh, Batu Gajah, Kampar</option>
        <option value="PRK03">Lenggong, Pengkalan Hulu, Grik</option>
        <option value="PRK04">Temengor, Belum</option>
        <option value="PRK05">Kg Gajah, Teluk Intan, Bagan Datuk, Seri Iskandar, Beruas, Parit,
          Lumut, Sitiawan, Pulau Pangkor</option>
        <option value="PRK06">Selama, Taiping, Bagan Serai, Parit Buntar</option>
        <option value="PRK07">Bukit Larut</option>
      </optgroup>
      <optgroup label="Sabah">
        <option value="SBH01">Bahagian Sandakan (Timur), Bukit Garam, Semawang, Temanggong, Tambisan,
          Bandar Sandakan, Sukau</option>
        <option value="SBH02">Beluran, Telupid, Pinangah, Terusan, Kuamut, Bahagian Sandakan (Barat)
        </option>
        <option value="SBH03">Lahad Datu, Silabukan, Kunak, Sahabat, Semporna, Tungku, Bahagian Tawau
          (Timur)</option>
        <option value="SBH04">Bandar Tawau, Balong, Merotai, Kalabakan, Bahagian Tawau (Barat)
        </option>
        <option value="SBH05">Kudat, Kota Marudu, Pitas, Pulau Banggi, Bahagian Kudat</option>
        <option value="SBH06">Gunung Kinabalu</option>
        <option value="SBH07">Kota Kinabalu, Ranau, Kota Belud, Tuaran, Penampang, Papar, Putatan,
          Bahagian Pantai Barat</option>
        <option value="SBH08">Pensiangan, Keningau, Tambunan, Nabawan, Bahagian Pendalaman (Atas)
        </option>
        <option value="SBH09">Beaufort, Kuala Penyu, Sipitang, Tenom, Long Pasia, Membakut, Weston,
          Bahagian Pendalaman (Bawah)</option>
      </optgroup>
      <optgroup label="Selangor">
        <option value="SGR01">Gombak, Petaling, Sepang, Hulu Langat, Hulu Selangor, S.Alam</option>
        <option value="SGR02">Kuala Selangor, Sabak Bernam</option>
        <option value="SGR03">Klang, Kuala Langat</option>
      </optgroup>
      <optgroup label="Sarawak">
        <option value="SWK01">Limbang, Lawas, Sundar, Trusan</option>
        <option value="SWK02">Miri, Niah, Bekenu, Sibuti, Marudi</option>
        <option value="SWK03">Pandan, Belaga, Suai, Tatau, Sebauh, Bintulu</option>
        <option value="SWK04">Sibu, Mukah, Dalat, Song, Igan, Oya, Balingian, Kanowit, Kapit</option>
        <option value="SWK05">Sarikei, Matu, Julau, Rajang, Daro, Bintangor, Belawai</option>
        <option value="SWK06">Lubok Antu, Sri Aman, Roban, Debak, Kabong, Lingga, Engkelili, Betong,
          Spaoh, Pusa, Saratok</option>
        <option value="SWK07">Serian, Simunjan, Samarahan, Sebuyau, Meludam</option>
        <option value="SWK08">Kuching, Bau, Lundu, Sematan</option>
        <option value="SWK09">Zon Khas (Kampung Patarikan)</option>
      </optgroup>
      <optgroup label="Terengganu">
        <option value="TRG01">Kuala Terengganu, Marang, Kuala Nerus</option>
        <option value="TRG02">Besut, Setiu</option>
        <option value="TRG03">Hulu Terengganu</option>
        <option value="TRG04">Dungun, Kemaman</option>
      </optgroup>
      <optgroup label="Wilayah Persekutuan">
        <option value="WLY01">Kuala Lumpur, Putrajaya</option>
        <option value="WLY02">Labuan</option>
      </optgroup>
    </select>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue';

const props = defineProps({
  modelValue: String,
  bearing: String
})

defineEmits(['update:modelValue'])

let zoneList = {
  JHR01: 'Pulau Aur dan Pulau Pemanggil',
  JHR02: 'Johor Bahru, Kota Tinggi, Mersing, Kulai',
  JHR03: 'Kluang, Pontian',
  JHR04: 'Batu Pahat, Muar, Segamat, Gemas Johor, Tangkak',
  KDH01: 'Kota Setar, Kubang Pasu, Pokok Sena (Daerah Kecil)',
  KDH02: 'Kuala Muda, Yan, Pendang',
  KDH03: 'Padang Terap, Sik',
  KDH04: 'Baling',
  KDH05: 'Bandar Baharu, Kulim',
  KDH06: 'Langkawi',
  KDH07: 'Puncak Gunung Jerai',
  KTN01: 'Bachok, Kota Bharu, Machang, Pasir Mas, Pasir Puteh, Tanah Merah, Tumpat, Kuala Krai, Mukim Chiku',
  KTN02: 'Gua Musang (Daerah Galas Dan Bertam), Jeli, Jajahan Kecil Lojing',
  MLK01: 'Seluruh Negeri Melaka',
  NGS01: 'Tampin, Jempol',
  NGS02: 'Jelebu, Kuala Pilah, Rembau',
  NGS03: 'Port Dickson, Seremban',
  PHG01: 'Pulau Tioman',
  PHG02: 'Kuantan, Pekan, Rompin, Muadzam Shah',
  PHG03: 'Jerantut, Temerloh, Maran, Bera, Chenor, Jengka',
  PHG04: 'Bentong, Lipis, Raub',
  PHG05: 'Genting Sempah, Janda Baik, Bukit Tinggi',
  PHG06: 'Cameron Highlands, Genting Higlands, Bukit Fraser',
  PLS01: 'Kangar, Padang Besar, Arau',
  PNG01: 'Seluruh Negeri Pulau Pinang',
  PRK01: 'Tapah, Slim River, Tanjung Malim',
  PRK02: 'Kuala Kangsar, Sg. Siput, Ipoh, Batu Gajah, Kampar',
  PRK03: 'Lenggong, Pengkalan Hulu, Grik',
  PRK04: 'Temengor, Belum',
  PRK05: 'Kg Gajah, Teluk Intan, Bagan Datuk, Seri Iskandar, Beruas, Parit, Lumut, Sitiawan, Pulau Pangkor',
  PRK06: 'Selama, Taiping, Bagan Serai, Parit Buntar',
  PRK07: 'Bukit Larut',
  SBH01: 'Bahagian Sandakan (Timur), Bukit Garam, Semawang, Temanggong, Tambisan, Bandar Sandakan, Sukau',
  SBH02: 'Beluran, Telupid, Pinangah, Terusan, Kuamut, Bahagian Sandakan (Barat)',
  SBH03: 'Lahad Datu, Silabukan, Kunak, Sahabat, Semporna, Tungku, Bahagian Tawau (Timur)',
  SBH04: 'Bandar Tawau, Balong, Merotai, Kalabakan, Bahagian Tawau (Barat)',
  SBH05: 'Kudat, Kota Marudu, Pitas, Pulau Banggi, Bahagian Kudat',
  SBH06: 'Gunung Kinabalu',
  SBH07: 'Kota Kinabalu, Ranau, Kota Belud, Tuaran, Penampang, Papar, Putatan, Bahagian Pantai Barat',
  SBH08: 'Pensiangan, Keningau, Tambunan, Nabawan, Bahagian Pendalaman (Atas)',
  SBH09: 'Beaufort, Kuala Penyu, Sipitang, Tenom, Long Pasia, Membakut, Weston, Bahagian Pendalaman (Bawah)',
  SGR01: 'Gombak, Petaling, Sepang, Hulu Langat, Hulu Selangor, S.Alam',
  SGR02: 'Kuala Selangor, Sabak Bernam',
  SGR03: 'Klang, Kuala Langat',
  SWK01: 'Limbang, Lawas, Sundar, Trusan',
  SWK02: 'Miri, Niah, Bekenu, Sibuti, Marudi',
  SWK03: 'Pandan, Belaga, Suai, Tatau, Sebauh, Bintulu',
  SWK04: 'Sibu, Mukah, Dalat, Song, Igan, Oya, Balingian, Kanowit, Kapit',
  SWK05: 'Sarikei, Matu, Julau, Rajang, Daro, Bintangor, Belawai',
  SWK06: 'Lubok Antu, Sri Aman, Roban, Debak, Kabong, Lingga, Engkelili, Betong, Spaoh, Pusa, Saratok',
  SWK07: 'Serian, Simunjan, Samarahan, Sebuyau, Meludam',
  SWK08: 'Kuching, Bau, Lundu, Sematan',
  SWK09: 'Zon Khas (Kampung Patarikan)',
  TRG01: 'Kuala Terengganu, Marang, Kuala Nerus',
  TRG02: 'Besut, Setiu',
  TRG03: 'Hulu Terengganu',
  TRG04: 'Dungun, Kemaman',
  WLY01: 'Kuala Lumpur, Putrajaya',
  WLY02: 'Labuan',
}

const zoneName = computed(() => {
  return zoneList[props.modelValue]
})
</script>