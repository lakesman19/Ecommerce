<template>
  <MainLayouts>
    <div id="IndexPage" class="mt-4 max-w-[1200px] mx-auto px-2">
      <div
        class="grid xl:grid-cols-6 lg:grid-cols-5 md:grid-cols-4 sm:grid-cols-3 grid-cols-2 gap-4"
      >
        <div v-for="product in products" :key="product">
          <ProductComponents :product="product" />
        </div>
      </div></div
  ></MainLayouts>
</template>

<script setup>
import MainLayouts from "~/layouts/MainLayouts.vue";
import ProductComponents from "~/components/ProductComponents.vue";
import { useUserStore } from "~/stores/user";

const userStore = useUserStore();
let products = ref(null);

onBeforeMount(async () => {
  try {
    const response = await fetch("https://api.escuelajs.co/api/v1/products");
    if (response.status === 200) {
      const data = await response.json();
      products.value = data;
      setTimeout(() => (userStore.isLoading = false), 1000);
    } else {
      console.log("Error: Unable to fetch data");
      userStore.isLoading = false;
    }
  } catch (error) {
    console.error(error);
    userStore.isLoading = false;
  }
});
</script>

<!-- // fetch("https://fakestoreapi.com/products")
  //   .then((res) => res.json())
  //   .then((json) => console.log("p-data", json)); -->
  <!-- // onBeforeMount(async () => {
//   products.value = await useFetch("https://fakestoreapi.com/products");
//   setTimeout(() => (userStore.isLoading = false), 1000);
//   console.log(products);
// }); -->