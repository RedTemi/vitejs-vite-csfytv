<template>
  <li>
    Name: {{ penguin.name }} rating: {{ penguin.rating }}
  </li>
</template>

<script>
export default {
  props: {
    penguin: {
      type: Object,
      default: () => ({}),
    },
  },
};
</script>
