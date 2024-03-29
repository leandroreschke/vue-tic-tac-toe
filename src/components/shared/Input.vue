<template>
  <div className="input">
    <input
      :id="id"
      :name="name"
      :type="type"
      :size="size"
      placeholder=" "
      :maxLength="maxLength"
      @keypress="keypress"
      @focus="focus"
      v-model="computedValue"
      :required="required"
      :readonly="readonly"
      :autocomplete="computedAutocomplete"
    />
    <label :for="id">{{ label }}</label>
  </div>
</template>

<script setup>

import { computed } from '@vue/reactivity';
import { RandomID } from '../../utility/Helpers';

const id = RandomID()

const props = defineProps({
  name: String, 
  label: String, 
  type: String, 
  size: String, 
  maxLength: String, 
  keypress: Function, 
  focus: Function, 
  required: Boolean, 
  readonly: Boolean, 
  modelValue: {
    default: '',
    type: String
  },
  reference, 
  autocomplete
})

defineEmits(['update:modelValue'])

const computedValue = computed({
  get(){
    return props.modelValue
  },
  set(value){
    emit('update:modelValue', value)
  }
})

const computedAutocomplete = computed(() => props.autocomplete ? 'on' : 'off')

</script>

<style scoped>

.input {
  display: inline-flex;
  position: relative;
  flex-direction: column;
}

.input > input {
  outline: none;
  appearance: none;
  background: transparent;
  border: .1rem solid hsla(var(--border));
  font-size: 1.6rem;
  margin-top: 2.5em;
  padding: .75em .75em;
  color: hsl(var(--text-color));
  border-radius: .4em;
  transition: border 0.3s ease, background 0.3s ease;

  width: 100%;
  height: inherit;

  max-width: inherit;
  max-height: inherit;

  min-width: 0;
  min-height: inherit;
  
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  text-overflow: ellipsis;
}

.input > input:-webkit-autofill,
.input > input:-webkit-autofill:hover, 
.input > input:-webkit-autofill:focus, 
.input > input:-webkit-autofill:active {
  background: transparent;
}

.input > input::-moz-placeholder {
  color: hsla(var(--border));
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.input > input:-ms-input-placeholder {
  color: hsla(var(--border));
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.input > input::placeholder {
  color: hsla(var(--border));
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.input > input::-webkit-calendar-picker-indicator {
  filter: invert(-1);
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.input > input:focus {
  outline: none;
  border-color: hsl(var(--primary-bg-color));
  background: hsla(var(--primary-bg-color), .15);
  color: hsla(var(--primary-text-color));
}

.input > input:not(:placeholder-shown):not(:focus) + label {
  transform: translate(.2em, .6em);
  font-weight: bold;
  color: hsla(var(--text-color-headline));
}

.input > input:focus + label,
.input > input:not(:placeholder-shown):focus + label {
  transform: translate(.2em, .6em);
  font-weight: bold;
  color: hsla(var(--primary-text-color));
}

.input > label {
  position: absolute;
  transform: translate(.8125em, 3.175em);
  color: hsl(var(--border));
  transition: all 0.2s ease-out;
  pointer-events: none;
  font-size: 1.6rem;
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

</style>