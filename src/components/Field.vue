<template>
  <input v-if="!as || as === 'input'" :type="type" :name="name" :placeholder="placeholder" v-model="fieldValue">
  <textarea v-else-if="as === 'textarea'" :name="name" :placeholder="placeholder" v-model="fieldValue"></textarea>
  <select v-else-if="as === 'select'" :name="name" v-model="fieldValue">
    <slot></slot>
  </select>
  <component v-else :is="as" :name="name"></component>
</template>

<script setup>
import {ref, onBeforeMount, inject, reactive, watch} from "vue";
import inputTypes from "@/utils/inputTypes.js";
const props = defineProps({
  as: {
    type: [String, Object],
    required: false,
    default: "input"
  },
  name: {
    type: String,
    required: true
  },
  placeholder: {
    type: String,
    required: false,
    default: null
  },
  type: {
    type: String,
    required: false,
    default: 'text',
    validator(value) {
      return inputTypes.includes(value)
    }
  },
});

const fieldValue = ref("");
const updateValue = inject("updateValue");
onBeforeMount(() => {
  const initialValues = inject('initialValues')
  if (initialValues && initialValues[props.name]) {
    fieldValue.value = initialValues[props.name]
  }
})

watch(fieldValue, (value) => {
  updateValue(props.name, value);
})


</script>
<style scoped></style>
