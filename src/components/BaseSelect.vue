<template>
  <label v-if="label">{{ label }}</label>
  <select
    :value="modelValue"
    @change="$emit('update:modelValue', $event.target.value)"
  >
    <option
      v-for="option in options"
      :value="option"
      :key="option"
      :selected="option === modelValue"
    >
      {{ option }}
    </option>
  </select>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
      required: true,
    },
    label: {
      type: String,
      default: '',
    },
    modelValue: {
      type: [String, Number],
    },
  },
};
</script>
