<template>
  <button @click="$emit('on-click')" :style="{ background: color }" class="btn">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "MyButton",
  props: {
    text: String,
    color: String,
  },
  emits: ["on-click"],
};
</script>
