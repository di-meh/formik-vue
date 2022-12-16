<template>
  <slot></slot>
</template>

<script setup>
import {provide, reactive} from "vue";

const props = defineProps({
  initialValues: {
    type: Object,
    required: true,
    default: {}
  },
  onSubmit: {
    type: Function,
    required: true
  },
  validate: {
    type: Function,
    required: false,
    default: null
  }
});
const values = reactive(props.initialValues);
provide('initialValues', values);

</script>

<style scoped>

</style>