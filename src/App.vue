<script setup>
import Field from "./components/Field.vue";
import Formik from "./components/Formik.vue";
import Captcha from "./components/Captcha.vue";
import {toRaw} from "vue";

// Cher Karl (ou à qui de droit),
// Je m'excuse d'avance pour les toRaw partout, mais je n'ai pas trouvé d'autre solution,
// Je sais que c'est possible d'avoir les valeurs de refs d'objets, mais à chaque fois ça me renvoyait un Proxy.
// Si jamais tu lis ce message, je serais ravi d'avoir ton retour sur ce point, pour pas que je meure bête.

// Merci d'avance. - Mehdi

const options = [
  { value: "1", label: "Option 1" },
  { value: "2", label: "Option 2" },
  { value: "3", label: "Option 3" },
];

const captchaOptions = [
  {
    id: 1,
    img: "https://picsum.photos/200?random=1",
  },
  {
    id: 2,
    img: "https://picsum.photos/200?random=2",
  },
  {
    id: 3,
    img: "https://picsum.photos/200?random=3",
  },
  {
    id: 4,
    img: "https://picsum.photos/200?random=4",
  },
  {
    id: 5,
    img: "https://picsum.photos/200?random=5",
  },
  {
    id: 6,
    img: "https://picsum.photos/200?random=6",
  },
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
<!--    <Field name="captcha" :as="Captcha" :options="captchaOptions"/>-->
    <button type="submit">Submit</button>
  </Formik>

</template>

<style>

</style>
