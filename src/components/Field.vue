<script setup>
    defineProps({
        type: {
            type: String,
            required: true,
            default: "email"
        },
        name: {
            type: String,
            required: true,
            default: "email"
        },
        options: {
            type: Array,
            required: false,
            default: []
        }
    })
</script>


<template>
    <input v-if="type === email" :type="type" :name="name">
    <select v-else :name="name">
        <option v-for="option in options" :value="option.value">
            {{ option.label }}
        </option>
    </select>
</template>

<style scoped></style>