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
  }
});

const values = reactive(inject("formValues"));

const isNotValidInput = () => {
  return !inputType.includes(props.type);
};
</script>

<template>
  <div v-if="isNotValidInput()">Toto</div>
  <div v-else>
    <label :for="name">{{ name }}</label>
    <input
      v-if="type !== 'select'"
      :type="type"
      :name="name"
      v-model="values[type]"
    />
    <select v-else :name="name" v-model="values[type]">
      <slot></slot>
    </select>
  </div>
</template>

<style scoped></style>
