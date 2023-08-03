<template>
  <div class="container py-[8px] px-[16px]">
    <div
      v-for="messenger in messengers"
      :key="messenger.name"
      @click="$emit('selectMessenger', messenger.name)"
      class="messenger-item"
    >
      <img :src="messenger.img" :alt="messenger.name" class="img" />
      <div>
        {{ messenger.name }}
      </div>
    </div>
  </div>
</template>

<script setup>
const messengers = [
  {
    name: 'WhatsApp',
    img: 'src/components/icons/WhatsApp.svg'
  },
  {
    name: 'Telegram',
    img: 'src/components/icons/Telegram.svg'
  },
  {
    name: 'Viber',
    img: 'src/components/icons/Viber.svg'
  },
  {
    name: 'SMS',
    img: 'src/components/icons/SMS.svg'
  }
]
</script>

<style scoped>
.container {
  border-radius: 4px;
  background: var(--login-android-day-c-7, #fff);
  box-shadow: 0px 3px 14px 2px rgba(0, 0, 0, 0.12), 0px 8px 10px 1px rgba(0, 0, 0, 0.14),
    0px 5px 5px -3px rgba(0, 0, 0, 0.2);
}
.messenger-item {
  @apply flex h-[48px] items-center;
}
.img {
  @apply mr-[10px] w-[24px] h-[24px];
}
</style>