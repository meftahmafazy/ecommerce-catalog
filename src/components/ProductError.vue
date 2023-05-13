<template>
  <div class="error-container">
    <div class="error"></div>
    <p>This product is unavailable to show</p>
    <div class="next-btn error-btn" @click="resetProduct()">Next Product</div>
  </div>
</template>
<script>
export default {
  name: "ProductError",
  methods: {
    resetProduct() {
      this.$emit("resetProduct");
    },
  },
  emits: ["resetProduct"],
};
</script>
