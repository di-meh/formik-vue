<script setup>
import Field from "./components/Field.vue";
import Formik from "./components/Formik.vue";

const options = [
  { value: "1", label: "Option 1" },
  { value: "2", label: "Option 2" },
  { value: "3", label: "Option 3" },
];
const initialValues = {
  email: "test@test.com",
  password: "password",
};

const submit = (values) => {
  console.log(values);
};

const validate = (values) => {
  console.log(values);
};
</script>

<template>
  <header>
    <h1>Formulaire</h1>
  </header>

  <main class="main">
    <Formik
      v-slot="slotProps"
      :initial-values="initialValues"
      :on-submit="submit"
      :validate="validate"
    >
      <Field type="email" name="email" />
      <Field type="password" name="password" />
      <button type="submit">Valider</button>
    </Formik>
  </main>
</template>

<style>

</style>
