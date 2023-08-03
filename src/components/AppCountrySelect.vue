<template>
  <div class="relative">
    <div
      @click="() => (modal = !modal)"
      class="text-field text-field_floating text-field__icon_component text-field__icon_arrow"
    >
      <input
        v-if="country"
        class="text-field__input cursor-pointer mb-[40px]"
        type="text"
        id="country"
        name="country"
        :placeholder="$t('placeholders.country')"
        :value="selectedCountry"
        disabled
      />
      <label v-if="country" class="text-field__label" for="email">{{
        $t('placeholders.country')
      }}</label>
      <input
        v-if="messenger"
        class="text-field__input cursor-pointer mb-[40px]"
        type="text"
        id="country"
        name="country"
        :placeholder="$t('placeholders.codeMethod')"
        :value="selectedMethod"
        disabled
      />
      <label v-if="messenger" class="text-field__label" for="email">{{
        $t('placeholders.codeMethod')
      }}</label>
    </div>
    <div>
      <CountrySearchModal
        v-if="modal && country"
        @selectCountry="selectCountry"
        class="absolute top-[50px] w-[440px] z-50"
      />
      <MessengerModal
        v-if="modal && messenger"
        class="absolute top-[50px] z-50"
        @selectMessenger="selectMessenger"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

import CountrySearchModal from './AppCountrySearchModal.vue'
import MessengerModal from './MessengersModal.vue'

const emit = defineEmits(['selectMessenger'])
const modal = ref(false)
const selectedCountry = ref('Russia')
const selectedMethod = ref('WhatsApp')
const selectCountry = function (country) {
  selectedCountry.value = country
  modal.value = false
}
const selectMessenger = function (messenger) {
  emit('selectMessenger', messenger)
  selectedMethod.value = messenger
  modal.value = false
}
defineProps({
  country: Boolean,
  messenger: Boolean
})
</script >

<style scoped>
input[type='text'],
textarea {
  background-color: #fff;
}
.text-field__icon_component {
  position: relative;
}
.text-field__icon_component::before {
  content: '';
  color: #bdbdbd;
  position: absolute;
  display: flex;
  align-items: center;
  top: 0;
  bottom: 0;
  right: 15px;
  top: 50%;
  transform: translateY(-50%);
}
.text-field__icon_arrow::before {
  width: 1rem;
  background-image: url(./icons/ArrowIcon.svg);
  background-repeat: no-repeat;
  background-position: center;
}
</style>
