<script setup>
import {inject} from "vue";

defineProps({
  name: {
    type: String,
    required: true,
  },
  options: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(["updateFormikValue"]);

function handleClick(value) {
  emit("updateFormikValue", value);
}

const formValues = inject("formValues");
</script>

<template>
  <div class="grid">
    <div
        :class="['grid-item', { selected: formValues[name] === option.id }]"
        v-for="option in options"
    >
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
