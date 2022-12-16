<script setup>
import Field from "./components/Field.vue";
import Formik from "./components/Formik.vue";
import { ref } from "vue";

const options = [
  { value: "1", label: "Option 1" },
  { value: "2", label: "Option 2" },
  { value: "3", label: "Option 3" },
];
const isSubmit = ref(false);
const initialValues = {
  email: "test@test.com",
  password: "password",
};

const submit = (values) => {
  console.log(values, "submit fonction");
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
};
</script>

<template>
  <header>
    <h1>He ça formik ou pas</h1>
  </header>

  <main class="container">
    <Formik
      :initial-values="initialValues"
      :on-submit="submit"
      :validate="validate"
      :is-submit="isSubmit"
      @submitted="isSubmit = false"
    >
      <Field type="email" name="email" />
      <Field type="password" name="password" />
      <Field type="select" name="select">
        <option v-for="option in options" :value="option.value">
          {{ option.label }}
        </option>
      </Field>
      <button type="submit" @click="handleSubmit">Submit</button>
    </Formik>
  </main>
</template>

<style>
.header {
  background-color: #f1f1f1;
  padding: 30px;
  text-align: center;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
</style>
