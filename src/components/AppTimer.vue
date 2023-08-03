<template>
  <span>
    <div v-if="timer > 9" class="text-[14px] text-[#9E9E9E]">0:{{ timer }}</div>
    <div v-else-if="timer > 0" class="text-[14px] text-[#9E9E9E]">0:0{{ timer }}</div>
    <div
      v-else
      @click="
        setTimer();$emit('sendCode')
      "
      class="text-[14px] text-[#007AFF]"
    >
      Отправить
    </div>
  </span>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const timer = ref(59)

const setTimer = function () {
  timer.value = 59
  let interval = setInterval(() => {
    if (timer.value === 0) {
      clearInterval(interval)
    } else {
      timer.value--
    }
  }, 1000)
}

onMounted(() => {
  setTimer()
})

</script>