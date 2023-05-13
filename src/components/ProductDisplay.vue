<template>
  <LoadingProduct v-if="loading" />
  <div class="container">
    <div class="product-image">
      <img :src="product.image" alt="Product Image" class="product-image" />
    </div>
    <div class="product-body">
      <div class="product-header">
        <h1 class="product.category === 'women\'s clothing' ? 'text-color-purple' : product.category === 'men\'s clothing' ? 'text-color-blue' : ''">{{ product.title }}></h1>
        <div class="product-category">
          <span>{{ product.category }}</span>
          <div class="product-rating">
            <span>{{ product.rating.rate }}/5</span>
            <div v-if="product.category === 'women\'s clothing'" class="product-rating-circles">
              <PurpleCircle v-for="(star, index) in Math.floor(product.rating.rate)" :key="index + star" />
              <WhiteCircle v-for="(star, index) in 5 - Math.floor(product.rating.rate)" :key="index + star" />
            </div>
            <div v-else-if="product.category === 'men\'s clothing'" class="product-rating-circles">
              <BlueCircle v-for="(star, index) in Math.floor(product.rating.rate)" :key="index + star" />
              <WhiteCircle v-for="(star, index) in 5 - Math.floor(product.rating.rate)" :key="index + star" />
            </div>
          </div>
        </div>
      </div>
      <div class="product-main">
        <p>
          {{ product.description }}
        </p>
      </div>
      <div class="product-footer">
        <h2 class="product.category === 'women\'s clothing' ? 'text-color-purple' : product.category === 'men\'s clothing' ? 'text-color-blue' : ''">${{ product.price }}></h2>
        <div class="product-buttons">
          <div :class="{ 'buy-btn buy-btn-purple': product.category === 'women\'s clothing', 'buy-btn buy-btn-blue': product.category === 'men\'s clothing' }">Buy now</div>
          <div :class="{ 'next-btn next-btn-purple': product.category === 'women\'s clothing', 'next-btn next-btn-blue': product.category === 'men\'s clothing' }" @click="nextProduct()">Next product</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import PurpleCircle from "./PurpleCircle.vue";
import WhiteCircle from "./WhiteCircle.vue";
import BlueCircle from "./BlueCircle.vue";
import LoadingProduct from "./ProductLoading.vue";

export default {
  name: "ProductDisplay",
  components: {
    PurpleCircle,
    WhiteCircle,
    BlueCircle,
    LoadingProduct,
  },
  props: {
    product: {
      type: Object,
      required: true,
    },
    productNumber: {
      type: Number,
      required: true,
    },
    loading: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    nextProduct() {
      this.$emit("nextProduct");
    },
  },
  emits: ["nextProduct"],

  data() {
    return {};
  },
};
</script>
