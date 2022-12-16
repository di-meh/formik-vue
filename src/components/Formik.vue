<script setup>
import { provide, onUpdated } from "vue";
const emit = defineEmits(['submitted']);

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
  isSubmit: {
    type: Boolean,
    required: true,
  }
});

provide("formValues", props.initialValues);

onUpdated(() => {
  if (props.isSubmit) {
    const errors = props.validate(props.initialValues);
    if (Object.keys(errors).length === 0) {
        props.onSubmit(props.initialValues);
        emit('submitted');
    }else{
        console.log(errors, "errors");
    }
  }
});
</script>

<template>
  <slot></slot>
</template>
