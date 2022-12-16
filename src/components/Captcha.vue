<script setup>
defineProps({
  captcha: {
    type: Object,
    required: true,
  },
  name: {
    type: String,
    required: true,
  },
  options: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits({
  "updateFormikValue": function validator(value) {
    return typeof value === "object" && value.id && value.img;
  },
  toto: () => true,
});

function handleClick(value) {
  emit("updateFormikValue", value);
}
</script>

<template>
  <div class="grid">
    <div
        :class="['grid-item', { selected: modelValue?.id === option.id }]"
        v-for="option in options"
    >
      <!--img :src="option.img" @click="$emit('update:modelValue', option)" /-->
      <img
          :src="option.img"
          @click.exact="handleClick(option.id)"
      />
    </div>
  </div>
</template>

<style scoped>
.grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
.grid-item {
  width: 30%;
}

.selected {
  border: 10px dashed magenta;
}
</style>
