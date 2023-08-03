<template>
  <div class="modal px-[16px] pt-[16px] pb-[8px] bg-white">
    <div>
      <Input
        class="mb-[16px]"
        :placeholder="$t('placeholders.search')"
        inputType="text"
        :icon="true"
        :grayBg="true"
        :noBorder="true"
        v-model="searchQuery"
      />
      <div class="" v-if="searchedCountries.length !== 0">
        <country-item
          v-for="country in searchedCountries"
          :key="country.code"
          :CountryCode="country.dial_code"
          :CountryFlag="country.flag"
          :CountryName="country.name"
          @click="$emit('selectCountry', country.name)"
        />
      </div>
      <div v-else class="text-center font-normal text-[#9E9E9E] h-[48px] leading-[48px]">Ничего не найдено</div>
    </div>
  </div>
</template>

<script setup>
import { useI18n } from 'vue-i18n'
import { ref, reactive, computed } from 'vue'
import Input from './AppInpuit.vue'
import CountryItem from './CountryItem.vue'
import countries from '../i18n/countriesEn.json'

const selectedCountry = ref('')
const searchQuery = ref('')

const searchedCountries = computed(() => {
  return countries
    .filter((country) => {
      return country.name.toLowerCase().indexOf(searchQuery.value.toLowerCase()) != -1
    })
    .slice(0, 5)
})

defineEmits(['update:modelValue'])
const { t } = useI18n({ useScope: 'global' })
const props = defineProps({
  modelValue: String
})
</script>

<style scoped>
.modal {
  border-radius: 4px;
  box-shadow: 0px 3px 14px 2px rgba(0, 0, 0, 0.12), 0px 8px 10px 1px rgba(0, 0, 0, 0.14),
    0px 5px 5px -3px rgba(0, 0, 0, 0.2);
}
</style>