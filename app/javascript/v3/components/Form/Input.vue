<script setup>
import { computed } from 'vue';
import { useToggle } from '@vueuse/core';

import Button from 'dashboard/components-next/button/Button.vue';
import WithLabel from './WithLabel.vue';

const props = defineProps({
  label: {
    type: String,
    required: true,
  },
  type: {
    type: String,
    default: 'text',
  },
  icon: {
    type: String,
    default: '',
  },
  name: {
    type: String,
    required: true,
  },
  hasError: Boolean,
  errorMessage: {
    type: String,
    default: '',
  },
  spacing: {
    type: String,
    default: 'base',
    validator: value => ['base', 'compact'].includes(value),
  },
});

const FIELDS = {
  TEXT: 'text',
  PASSWORD: 'password',
};

defineOptions({
  inheritAttrs: false,
});

const model = defineModel({
  type: [String, Number],
  required: true,
});

const [isPasswordVisible, togglePasswordVisibility] = useToggle();

const isPasswordField = computed(() => props.type === FIELDS.PASSWORD);

const currentInputType = computed(() => {
  if (isPasswordField.value) {
    return isPasswordVisible.value ? FIELDS.TEXT : FIELDS.PASSWORD;
  }
  return props.type;
});
</script>

<template>
  <WithLabel
    :label="label"
    :icon="icon"
    :name="name"
    :has-error="hasError"
    :error-message="errorMessage"
  >
    <template #rightOfLabel>
      <slot />
    </template>
    <input
      v-bind="$attrs"
      v-model="model"
      :name="name"
      :type="currentInputType"
      class="block w-full border-none rounded-md shadow-sm bg-slate-950/60 text-slate-100 placeholder:text-slate-500 sm:text-sm sm:leading-6 px-3 py-3 appearance-none outline outline-1 focus:outline focus:outline-1"
      :class="{
        'error outline-red-900/50 hover:outline-red-800 focus:outline-red-650':
          hasError,
        'outline-slate-800 hover:outline-slate-700 focus:outline-purple-500':
          !hasError,
        'px-3 py-3': spacing === 'base',
        'px-3 py-2 mb-0': spacing === 'compact',
        'pl-9': icon,
        'pr-10': isPasswordField,
      }"
    />
    <Button
      v-if="isPasswordField"
      type="button"
      slate
      sm
      link
      :icon="isPasswordVisible ? 'i-lucide-eye-off' : 'i-lucide-eye'"
      class="absolute inset-y-0 right-0 pr-3"
      :aria-label="isPasswordVisible ? 'Hide password' : 'Show password'"
      :aria-pressed="isPasswordVisible"
      @click="togglePasswordVisibility()"
    />
  </WithLabel>
</template>
