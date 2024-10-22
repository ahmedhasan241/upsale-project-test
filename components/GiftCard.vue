<template>
  <SwiperSlide class="!h-44 !relative">
    <div v-if="isDisabled" class="absolute top-0 left-0 w-full h-full background-overlay-gift">
      <div class="absolute top-3 right-3 h-4 md:!h-6 w-4 md:!w-6 rounded-full bg-gray-200 bg-opacity-50 flex items-center justify-center">
        <Icon name="material-symbols:lock-outline-sharp" class="!text-white text-[10px] md:!text-[14px]" />
      </div>
    </div>

    <Card
      class="cursor-pointer   p-2 h-full !w-full !rounded-lg transition-all duration-300 hover:shadow-lg card-shadow-gift"
      :class="{
        'border-2 border-black': selectedGifts.some(item => item.id === gift.id) || !isDisabled,
        'border-2 border-white': !selectedGifts.some(item => item.id === gift.id) || isDisabled,
      }"
      @click="toggleSelectGifts(gift)"
    >

      <template #header>
        <div class="w-full h-24 mb-2 relative card-image">
          <img class="object-contain h-full mx-auto" alt="product image" :src="gift.image" />
      
          <span
            v-if="discountPercentage(gift.price_before_discount, gift.price) > 0"
            class="discount-badge absolute top-2 left-2 bg-red-500 text-white px-2 py-1 rounded-full"
          >
            خصم {{ discountPercentage(gift.price_before_discount, gift.price) }}%
          </span>
        </div>
      </template>

      <template #title>
        <div class="flex flex-col gap-2">
          <h2 class="text-black font-almarai text-[14px] font-medium leading-[14.4px] tracking[-0.02em] text-center">{{ gift.name_ar }}</h2>
          <div class="flex flex-row justify-center gap-2 mt-1 !h-4">
            <p class="font-almarai text-[12px] font-bold">
              <span >{{ gift.price }}</span>
              <span  class="text-[10px] mx-1">ر.س</span>
            </p>
            <p class="font-almarai line-through text-[12px] text-gray-400 font-bold">
              <span >{{ gift.price_before_discount }}</span>
              <span  class="text-[10px] mx-1">ر.س</span>
            </p>
          </div>
        </div>
      </template>
    </Card>
  </SwiperSlide>
</template>

<script setup>
defineProps({
  gift: Object,
  selectedGifts: Array,
  isDisabled: Boolean,
  toggleSelectGifts: Function,
})

function discountPercentage(priceBeforeDiscount, currentPrice) {
  if (priceBeforeDiscount && currentPrice && priceBeforeDiscount > currentPrice) {
    const discount = ((priceBeforeDiscount - currentPrice) / priceBeforeDiscount) * 100;
    return Math.round(discount); // Return the rounded percentage
  }
  return 0; // No discount if conditions are not met
}
</script>


<style scoped>

.discount-badge {
  position: absolute;
  width: 55px;
  height: 20px;
  top: 3px;
  right: 0px;
  background-color: #000;
  color: white;
  border: 1px solid #fff;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  z-index: 10;
  font-family: "Almarai";
  font-size: 8px;
  font-weight: 400;
}

</style>