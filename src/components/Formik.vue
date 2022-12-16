<script setup>
import { provide } from 'vue'

    const props = defineProps({
        validate: {
            type: Function,
            required: false,
        },
        initialValues: {
            type: Object,
            required: false,
        },
        onSubmit: {
            type: Function,
            required: false
        }
    })

provide('initialValues', initialValues)

</script>


<template>
    <slot :values="initialValues"></slot>
</template>