<template>
  <TransitionRoot as="template" :show="enable">
    <Dialog as="div" class="relative z-10" @close="enable = false">
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
              <div class="bg-white px-4 pt-5 pb-4 sm:p-8 sm:pb-4">
                <div class="flex justify-center mb-3">
                  <InformationCircleIcon class="h-20 w-auto text-gray-500" aria-hidden="true" />
                </div>
                <h1 class="text-center font-semibold text-lg">
                  Waktu Solat hanya bagi Semenanjung Malaysia, Sabah dan Sarawak
                </h1>
              </div>
              <div class="bg-white px-4 py-3 flex justify-center items-center">
                <button type="button"
                  class="mt-3 inline-flex w-full justify-center rounded-md border border-gray-300 bg-gray-50 px-4 py-2 text-base font-medium text-gray-700 shadow-sm hover:bg-gray-50 focus:outline-none focus:border focus:ring-0 sm:mt-0 sm:ml-3 sm:w-auto sm:text-sm"
                  @click="enable = false" ref="cancelButtonRef">Tutup</button>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup>
import { Dialog, DialogPanel, TransitionChild, TransitionRoot } from '@headlessui/vue'
import { InformationCircleIcon } from '@heroicons/vue/24/outline'

const props = defineProps({
  enable: Boolean
})
</script>