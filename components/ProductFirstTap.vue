<script setup>
defineProps({
  card: Object,
  selected: String|Number
});
</script>

<template>
<div>
  <div class="flex flex-row justify-start mb-4">
    <h2 class="font-almarai text-[16px] font-semibold leading-[19.2px] text-right">
      {{ selected.name_ar }}
    </h2>
  </div>
  <div
      v-if="selected.description"
      class="description"
      v-html="selected.description"
  ></div>
  <div class="mt-4 flex justify-center" v-else>
    <h2 class="text-lg text-black text-bold">لا يوجد تفاصيل</h2>
  </div>
</div>
</template>

<style scoped lang="scss">

</style>