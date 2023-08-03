<template>
    <button
      class="w-full h-[55px] px-[16px] text-center leading-[55px] bg-[#007AFF] text-white rounded-[4px]"
    >
      {{ msg }}
    </button>
</template>

<script setup>
defineProps({
  msg: String
})
</script>