<script setup>

import Formik from "@/components/Formik.vue";
import Field from "@/components/Field.vue";
</script>

<template>

  <Formik>
    <Field name="test" as="input" type="text" />
    <Field name="test2" as="textarea" />
    <Field name="test3" as="select" :options="[{value: '1', label: 'One'}, {value: '2', label: 'Two'}]" />
  </Formik>

</template>

<style scoped>

</style>
