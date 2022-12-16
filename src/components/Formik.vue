<script setup>
import {provide, ref, reactive, toRaw} from "vue";
const props = defineProps({
  validate: {
    type: Function,
    required: false,
  },
  initialValues: {
    type: Object,
    required: true,
  },
  onSubmit: {
    type: Function,
    required: true,
  }
});

const isSubmitting = ref(false);
const errors = reactive([]);
const values = ref(props.initialValues);

const setSubmitting = (value) => isSubmitting.value = value;
const resetValues = () => values.value = props.initialValues;
const handleSubmit = () => {
  isSubmitting.value = true;
  if (props.validate) {
    Object.assign(errors, props.validate(values.value));
  }

  if (Object.keys(toRaw(errors)).length === 0) {
    props.onSubmit(values, {setSubmitting, resetValues});
  }
  else {
    isSubmitting.value = false;
    toRaw(errors).forEach((error) => console.error(error));
  }
  console.log(toRaw(values.value), "handleSubmit");
}
const updateValue = (name, value) => {
  values.value[name] = value;
}

provide("initialValues", props.initialValues);
provide("updateValue", updateValue);
provide("setSubmitting", setSubmitting);

// onUpdated(handleSubmit);
</script>

<template>
  <template v-if="!isSubmitting">
    <form @submit.prevent="handleSubmit">
      <slot></slot>
    </form>
  </template>
  <template v-else>
    <p>Submitting...</p>
  </template>
</template>

<style scoped>
  form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
</style>