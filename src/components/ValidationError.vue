<template>
  <ul class="list-group">
    <li
      v-for="errorMessage in errorMessages"
      :key="errorMessage"
      class="list-group-item list-group-item-danger mt-2"
    >
      {{ typeing }} {{ errorMessage }}
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    validationErrors: {
      type: Object,
      required: true,
    },
    typeing: {
      type: String,
      required: true,
    },
  },
  computed: {
    errorMessages() {
      return Object.keys(this.validationErrors).map((name) => {
        const msg = this.validationErrors.join(", ");
        return `${msg}`;
      });
    },
  },
};
</script>

<style></style>
