<template>
  <div
    class="text-field"
    :class="{
      'text-field_floating': floating,
      'text-field__icon': icon,
      'text-field__icon_search': icon
    }"
  >
    <input
      class="text-field__input"
      :class="{ gray_bg: grayBg, noBorder: noBorder }"
      :type="inputType"
      id="phone"
      name="phone"
      :placeholder="placeholder"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
    />
    <label v-if="floating" class="text-field__label" for="email">{{ placeholder }}</label>
  </div>
</template>

<script setup>
import { useI18n } from 'vue-i18n'
import { ref } from 'vue'

defineEmits(['update:modelValue'])
const { t } = useI18n({ useScope: 'global' })

const props = defineProps({
  inputType: String,
  modelValue: String,
  placeholder: String,
  floating: Boolean,
  icon: Boolean,
  inputColor: String,
  grayBg: Boolean,
  noBorder: Boolean
})
</script>

<style>
.text-field__label {
  display: block;
  margin-bottom: 0.25rem;
}

.text-field__input {
  display: block;
  width: 100%;
  height: calc(2.25rem + 2px);
  font-family: inherit;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5;
  padding-left: 30px;
  color: #212529;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #bdbdbd;
  border-radius: 0.25rem;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}
.gray_bg {
  background-color: #f8f8f8;
}

.noBorder {
  border-width: 0px;
}
.text-field__input[type='search']::-webkit-search-decoration,
.text-field__input[type='search']::-webkit-search-cancel-button,
.text-field__input[type='search']::-webkit-search-results-button,
.text-field__input[type='search']::-webkit-search-results-decoration {
  -webkit-appearance: none;
}

.text-field__input::placeholder {
  color: #212529;
  opacity: 0.4;
}

.text-field__input:focus {
  color: #212529;
  background-color: #fff;
  border-color: #bdbdbd;
  outline: 0;
}

.gray_bg:focus {
  background-color: #f8f8f8;
}

.text-field__input:disabled,
.text-field__input[readonly] {
  background-color: #f5f5f5;
  opacity: 1;
}

.text-field_floating {
  position: relative;
}

.text-field_floating .text-field__input {
  height: calc(2.5rem + 2px);
  padding: 0.5rem 0.75rem;
}

.text-field_floating .text-field__label {
  position: absolute;
  top: 50%;
  left: 0.3125rem;
  display: flex;
  transform: translateY(-50%);
  pointer-events: none;
  border: none;
  background-color: #fff;
  color: #757575;
  padding-left: 0.5rem;
  padding-right: 0.5rem;
  transition: top 0.1s ease-in-out, scale 0.1s ease-in-out;
}

.text-field_floating .text-field__input::-moz-placeholder {
  color: transparent;
}

.text-field_floating .text-field__input::placeholder {
  color: transparent;
}

.text-field_floating .text-field__input:focus ~ .text-field__label,
.text-field_floating .text-field__input:not(:placeholder-shown) ~ .text-field__label {
  top: 0;
  transform: translateY(-50%) scale(0.75);
}

.text-field__icon {
  position: relative;
}
.text-field__icon::before {
  content: '';
  color: #bdbdbd;
  position: absolute;
  display: flex;
  align-items: center;
  top: 0;
  bottom: 0;
  left: 10px;
  top: 50%;
  transform: translateY(-50%);
}
.text-field__icon_search::before {
  width: 1rem;
  background-image: url(./icons/SearchGlyph.svg);
  background-repeat: no-repeat;
  background-position: center;
}
</style>