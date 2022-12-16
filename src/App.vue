<script setup>
import Field from "./components/Field.vue";
import Formik from "./components/Formik.vue";
import { ref } from "vue";

const options = [
  { value: "1", label: "Option 1" },
  { value: "2", label: "Option 2" },
  { value: "3", label: "Option 3" },
];
const initialValues = {
  name: "John",
  email: "john@doe.com",
  password: "password",
  test3: 2
};
const isSubmit = ref(false);
const submit = (values) => {
  console.log(values);
};
const validate = (values) => {
  const errors = {};
  if (!values.email) {
    errors.email = "Required";
  } else if (!/\S+@\S+\.\S+/.test(values.email)) {
    errors.email = "Invalid email address";
  }
  return errors;
};
const handleSubmit = (event) => {
  event.preventDefault();
  isSubmit.value = true;
}
</script>

<template>
  <Formik :initial-values="initialValues" :on-submit="submit" :is-submit="isSubmit" :validate="validate" @submitted="isSubmit = false">
    <Field name="name" as="input" type="text" />
    <Field name="email" as="input" type="email" />
    <Field name="password" as="input" type="password" />
    <Field name="test3" as="select">
      <option v-for="option in options" :value="option.value">{{ option.label }}</option>
    </Field>
  </Formik>
  <button type="submit" @click="handleSubmit">Submit</button>
</template>

<style>

</style>
