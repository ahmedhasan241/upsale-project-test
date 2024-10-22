<template>

      <div v-if="isDisabled" class="absolute top-0 left-0 w-full h-full background-overlay-gift">
        <div class="absolute top-3 right-3 h-4 md:!h-6 w-4 md:!w-6 rounded-full bg-gray-200 bg-opacity-50 flex items-center justify-center">
          <Icon name="material-symbols:lock-outline-sharp" class="!text-white text-[10px] md:!text-[14px]" />
        </div>
      </div>
  
      <Card
        class="cursor-pointer p-2 h-full !w-full !rounded-lg"
        :class="{
          'border-2 border-black': selectedGifts.some(item => item.id === discountAmount.id) || !isDisabled,
          'border-2 border-white': !selectedGifts.some(item => item.id === discountAmount.id) || isDisabled
        }"
        @click="toggleSelectGifts(discountAmount)"
      >
        <template #header>
          <div class="w-full h-24 mb-2 card-image relative">
            <img class="object-contain h-full mx-auto" alt="discount image" :src="discountAmount.image" />
          </div>
        </template>
  
        <template #title>
          <h2 class="text-black font-almarai text-[14px] font-medium leading-[14.4px] tracking-[-0.02em] text-center">
            {{ discountAmount.name }}
          </h2>
        </template>
      </Card>
  </template>
  
  <script setup>
  defineProps({
    campaignInfo: Object,
    discountAmount: Object,
    selectedGifts: Array,
    isDisabled: Boolean,
    toggleSelectGifts: Function,
  })
  </script>
  

  <style>


</style>