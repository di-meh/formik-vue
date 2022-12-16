<script setup>
import { provide } from 'vue'
const props = defineProps({
  validate: {
    type: Function,
    required: true,
  },
  initialValues: {
    type: Object,
    required: false,
  },
  onSubmit: {
    type: Function,
    required: true,
  },
});
provide('initialValues', props.initialValues)
</script>

<template>
  <slot></slot>
</template>
