<script setup>
import { inputType } from "../enum";
import { reactive, inject } from "vue";
const props = defineProps({
  type: {
    type: String,
    required: true,
    default: "email",
  },
  name: {
    type: String,
    required: true,
    default: "email",
  },
  options: {
    type: Array,
    required: false,
    default: [],
  },
});

const values = reactive(inject("initialValues"));

const checkInput = () => {
  return !inputType.includes(props.type);
};
console.log(values);
</script>

<template>
  <div v-if="checkInput()">Wolverine</div>
  <div v-else>
    <label :for="name">{{ name }}</label>
    <input
      v-if="type !== 'select'"
      :type="type"
      :name="name"
      v-model="values[type]"
    />
    <select v-else :name="name" v-model="values[type]">
      <option v-for="option in options" :value="option.value">
        {{ option.label }}
      </option>
    </select>
  </div>
</template>

<style scoped></style>
