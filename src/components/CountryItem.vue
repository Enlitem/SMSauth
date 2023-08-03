<template>
  <div class="flex h-[48px] px-[16px] justify-between items-center">
    <div class="flex">
      <div class="mr-[10px]">{{ CountryFlag }}</div>
      <div class="">{{ CountryName }}</div>
    </div>
    <div class="font-bold">{{ CountryCode }}</div>
  </div>
</template>

<script setup>
defineProps({
  CountryName: String,
  CountryCode: String,
  CountryFlag: String
})
</script>

<style>
</style>