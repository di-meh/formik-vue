<template>
  <input v-if="!as || as === 'input'" :type="type" :name="name" :placeholder="placeholder" v-model="fieldValue">
  <textarea v-else-if="as === 'textarea'" :name="name" :placeholder="placeholder" v-model="fieldValue"></textarea>
  <select v-else-if="as === 'select' && options.length > 0" :name="name" v-model="fieldValue">
    <option v-for="option in options" :value="option.value" :key="option.value">{{ option.label }}</option>
  </select>
  <component v-else :is="as" :name="name"></component>
</template>

<script setup>
import {ref, onBeforeMount, inject} from "vue";
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
  options: {
    type: Array,
    required: false,
    default: null
  }
})

const fieldValue = ref('')

onBeforeMount(() => {
  const initialValues = inject('initialValues')
  if (initialValues) {
    fieldValue.value = initialValues[props.name]
  }
})
</script>

<style scoped>

</style>