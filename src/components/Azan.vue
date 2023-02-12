<template>
  <TransitionRoot as="template" :show="open">
    <Dialog as="div" class="relative z-10" @close="sendClickEvent">
      <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0" enter-to="opacity-100"
        leave="ease-in duration-200" leave-from="opacity-100" leave-to="opacity-0">
        <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" />
      </TransitionChild>

      <div class="fixed inset-0 z-10 overflow-y-auto">
        <div class="flex min-h-full items-center justify-center p-4 text-center sm:p-0">
          <TransitionChild as="template" enter="ease-out duration-300"
            enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            enter-to="opacity-100 translate-y-0 sm:scale-100" leave="ease-in duration-200"
            leave-from="opacity-100 translate-y-0 sm:scale-100"
            leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">
            <DialogPanel
              class="relative transform overflow-hidden rounded-lg bg-white text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg">
              <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
                <h1 class="text-center font-bold text-lg mb-4">Azan sedang berkumandang</h1>
                <div class="flex items-center justify-center">
                  <audio ref="audio" preload controls>
                    <source src="./../assets/azan.mp3" type="audio/mpeg">
                    Your browser does not support the audio element.
                  </audio>
                </div>
              </div>
              <div class="bg-white px-4 py-3 flex justify-center items-center">
                <button type="button"
                  class="mt-3 inline-flex w-full justify-center rounded-md border border-gray-300 bg-gray-50 px-4 py-2 text-base font-medium text-gray-700 shadow-sm hover:bg-gray-50 focus:outline-none focus:border focus:ring-0 sm:mt-0 sm:ml-3 sm:w-auto sm:text-sm"
                  @click="sendClickEvent" ref="cancelButtonRef">Tutup</button>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup>
import { ref, watchEffect } from 'vue';
import { Dialog, DialogPanel, TransitionChild, TransitionRoot } from '@headlessui/vue'

const props = defineProps({
  open: Boolean
})

const emit = defineEmits(["click-event"]);
const sendClickEvent = () => emit("click-event");

const audio = ref(null)

watchEffect(() => {
  if (audio.value) {
    audio.value.play()
  }
})
</script>