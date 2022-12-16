<script setup>
import Field from "./components/Field.vue";
import Formik from "./components/Formik.vue";
import {toRaw} from "vue";

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

const onSubmit = (values, { setSubmitting, resetValues }) => {
  setTimeout(() => {
    setSubmitting(false);
    console.log(toRaw(values.value), "onSubmit");
    resetValues();
  }, 1000);
};
const validate = (values) => {
  const errors = [];
  if (!values.email) {
    errors.push("Email is required");
  } else if (!/\S+@\S+\.\S+/.test(values.email)) {
    errors.push("Email is invalid");
  }
  // Mettez tout ce que vous voulez comme condition de validation ici

  return errors;
};

</script>

<template>
  <h1>Formik-Vue</h1>
  <h2>Par Mehdi SABER et Souleymane GUEYE</h2>
  <Formik :initial-values="initialValues" :on-submit="onSubmit" :validate="validate">
    <Field name="name" as="input" type="text" />
    <Field name="email" as="input" type="email" />
    <Field name="password" as="input" type="password" />
    <Field name="test3" as="select">
      <option v-for="option in options" :value="option.value">{{ option.label }}</option>
    </Field>
    <button type="submit">Submit</button>
  </Formik>

</template>

<style>

</style>
