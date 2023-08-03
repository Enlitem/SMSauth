<template>
  <div class="w-[500px] p-[30px] rounded-lg border border-[#DFDFDF] pt-[50px] pb-[24px]">
    <Logo class="mx-auto mb-[30px]" />
    <div class="mb-[30px]">
      <h1 v-if="stepPhoneNumber" class="title">
        {{ $t('titles.number') }}
      </h1>
      <h2 v-if="stepPhoneNumber" class="subtitle">{{ $t('subtitles.number') }}</h2>
      <h1 v-if="stepEnterCode" class="title">
        {{ $t('titles.code') }}
      </h1>
      <h2 v-if="stepEnterCode" class="subtitle">{{ $t('subtitles.code') }} +{{ phoneNumber }}</h2>
    </div>
    <CountrySelect v-if="stepPhoneNumber" :country="true" :messenger="false" class="mb-[40px]" />
    <CountrySelect
      v-if="stepEnterCode"
      :country="false"
      :messenger="true"
      class="mb-[40px]"
      @selectMessenger="(messenger) => messageType = messenger.toLowerCase()"
    />
    <Input
      v-if="stepPhoneNumber"
      inputType="tel"
      :placeholder="$t('placeholders.number')"
      :floating="true"
      :icon="false"
      v-model="phoneNumber"
      class="mb-[50px]"
    />
    <div v-if="stepEnterCode" class="relative">
      <Input
        inputType="number"
        :placeholder="$t('placeholders.enterCode')"
        :floating="true"
        :icon="false"
        v-model="code"
        class="mb-[50px]"
      />
      <Timer @sendCode="send()" class="absolute top-[10px] right-[16px]" />
    </div>
    <div class="px-[2px]">
      <Button
        v-if="stepPhoneNumber"
        @click="createSession"
        :msg="$t('buttons.continue')"
        class="mb-[70px]"
      />
      <div v-if="stepEnterCode" class="flex mb-[70px]">
        <button @click="goBack" class="flex w-full items-center justify-center mr-[10px]">
          <img src="./icons/ArrowBack.svg" class="mr-[10px]" />
          <div class="text-[#007AFF] font-medium">{{ $t('buttons.back') }}</div>
        </button>
        <Button @click="check" :msg="$t('buttons.continue')" />
      </div>
      <div class="flex justify-between">
        <div>{{ $t('language') }}</div>
        <div class="flex">
          <a href="#" class="mr-[24px]">{{ $t('conditions') }}</a>
          <a href="#">{{ $t('confidentiality') }}</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useI18n } from 'vue-i18n'
import { ref } from 'vue'

import Logo from './AppLogo.vue'
import Input from './AppInpuit.vue'
import Button from './AppButton.vue'
import CountrySelect from './AppCountrySelect.vue'
import Timer from './AppTimer.vue'

const { t } = useI18n({ useScope: 'global' })

const stepPhoneNumber = ref(true)
const stepEnterCode = ref(false)
const phoneNumber = ref('')
const messageType = ref('whatsapp')
const code = ref('')
const xApiKey = '09459085-5327-4ae9-85a8-214b7755fc2a'

const myHeaders = new Headers()
myHeaders.append('Accept', 'application/json')
myHeaders.append('Content-Type', 'application/json')
myHeaders.append('x-api-key', xApiKey)

const requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
}

const createSession = function () {
  fetch(
    `https://api.kod.mobi/api/v1/message/create?phone=${phoneNumber.value}&type=${messageType.value}`,
    requestOptions
  )
    .then((response) => response.text())
    .then((result) => {
      sessionStorage.setItem('sessionId', JSON.parse(result).data.session_id)
    })
    .then(() => {
      stepPhoneNumber.value = false
      stepEnterCode.value = true
    })
    .catch((error) => console.log('error', error))
  stepPhoneNumber.value = false
  stepEnterCode.value = true
}

const check = function () {
  fetch(
    `https://api.kod.mobi/api/v1/message/check?session_id=${sessionStorage.getItem(
      'sessionId'
    )}&code=${code.value}`,
    requestOptions
  )
    .then((response) => response.text())
    .then((result) => console.log(result))
    .catch((error) => console.log('error', error))
}

const send = function () {
  fetch(
    `https://api.kod.mobi/api/v1/message/send?session_id=${sessionStorage.getItem(
      'sessionId'
    )}&type=${messageType.value}`,
    requestOptions
  )
    .then((response) => response.text())
    .then((result) => console.log(result))
    .catch((error) => console.log('error', error))
}

const goBack = function () {
  stepPhoneNumber.value = true
  stepEnterCode.value = false
}
</script>

<style scoped>
.title {
  @apply text-center text-[32px] font-medium mb-[14px];
}

.subtitle {
  @apply text-center text-[#666];
}
</style>