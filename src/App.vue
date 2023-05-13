<template>
  <div class="bg-pattern-error"></div>
  <div v-if="product" :class="product.category === 'women\'s clothing' ? 'bg-pattern-pink' : product.category === 'men\'s clothing' ? 'bg-pattern-blue' : 'bg-pattern-lightgray'"></div>
  <div v-if="loading">
    <div class="home-loader">
      <HomeLoading />
    </div>
  </div>
  <div class="App">
    <div v-if="tampil">
      <ProductDisplay v-if="product" :product="product" :product-number="productNumber" :loading="loading" @nextProduct="setLoadingAndNextProduct(true)" />
    </div>
    <div v-else>
      <ProductError @resetProduct="setLoadingAndNextProduct(true)" />
    </div>
  </div>
</template>

<script>
import { ref, watchEffect } from "vue";
import "./assets/css/page.css";
import ProductDisplay from "./components/ProductDisplay.vue";
import HomeLoading from "./components/ProductLoading.vue";
import ProductError from "./components/ProductError.vue";

const product = ref(undefined);
const loading = ref(false);
const tampil = ref(false);
const productNumber = ref(1);
const error = ref(false);
const setLoadingAndNextProduct = (value) => {
  productNumber.value++;
  loading.value = value;
};
const setResetProduct = () => {
  productNumber.value = 1;
  loading.value = true;
  error.value = false;
};

export default {
  setup() {
    loading.value = true;
    tampil.value = false;
    watchEffect(() => {
      fetch(`https://fakestoreapi.com/products/${productNumber.value}`)
        .then((res) => res.json())
        .catch((err) => {
          error.value = true;
          loading.value = false;
          setResetProduct();
        })
        .then((data) => {
          if (data && (data.category == "men's clothing" || data.category == "women's clothing")) {
            tampil.value = true;
          } else {
            tampil.value = false;
          }
          product.value = data;
          loading.value = false;
        });
    });
  },
  data() {
    return {
      product,
      tampil,
      loading,
      productNumber,
      setLoadingAndNextProduct,
      error,
      setResetProduct,
    };
  },
  name: "App",
  components: {
    ProductDisplay,
    HomeLoading,
    ProductError,
  },
};
</script>
