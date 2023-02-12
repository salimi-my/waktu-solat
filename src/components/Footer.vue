<template>
  <footer class="w-full flex justify-center items-center">
    <div class="rounded-t-md bg-white/40 backdrop-blur-sm px-4 py-0 shadow-sm">
      <p class="font-normal">
        Waktu Solat &#169; {{ year }} Created by <a href="https://www.salimi.my" target="_blank" rel="noreferrer"
          class="hover:underline hover:font-semibold">Salimi</a>
      </p>
    </div>
  </footer>
</template>

<script setup>
const date = new Date();
const year = date.getFullYear();
</script>