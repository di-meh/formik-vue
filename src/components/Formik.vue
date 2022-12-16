<script setup>
import { objectToString } from '@vue/shared';


    const props = defineProps({
        validate: {
            type: Function,
            required: true,
        },
        initialValues: {
            type: Object,
            required: true,
        },
        onSubmit: {
            type: Function,
            required: true
        }
    })

</script>


<template>
    <slot :values="initialValues"></slot>
</template>