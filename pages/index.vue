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
// const products = [
//   {
//     id: 1,
//     title: "1",
//     description: "This is a description",
//     url: "https://piscum.photos/id/7/800/800",
//     price: 999,
//   },
//   {
//     id: 2,
//     title: "2",
//     description: "This is a description",
//     url: "https://piscum.photos/id/71/800/800",
//     price: 999,
//   },
//   {
//     id: 3,
//     title: "3",
//     description: "This is a description",
//     url: "https://piscum.photos/id/72/800/800",
//     price: 999,
//   },
//   {
//     id: 4,
//     title: "4",
//     description: "This is a description",
//     url: "https://piscum.photos/id/73/800/800",
//     price: 999,
//   },
//   {
//     id: 5,
//     title: "5",
//     description: "This is a description",
//     url: "https://piscum.photos/id/74/800/800",
//     price: 999,
//   },
//   {
//     id: 6,
//     title: "6",
//     description: "This is a description",
//     url: "https://piscum.photos/id/75/800/800",
//     price: 999,
//   },
//   {
//     id: 7,
//     title: "7",
//     description: "This is a description",
//     url: "https://piscum.photos/id/76/800/800",
//     price: 999,
//   },
//   {
//     id: 8,
//     title: "8",
//     description: "This is a description",
//     url: "https://piscum.photos/id/77/800/800",
//     price: 999,
//   },
//   {
//     id: 9,
//     title: "9",
//     description: "This is a description",
//     url: "https://piscum.photos/id/78/800/800",
//     price: 999,
//   },
//   {
//     id: 10,
//     title: "10",
//     description: "This is a description",
//     url: "https://piscum.photos/id/79/800/800",
//     price: 999,
//   },
// ];
const userStore = useUserStore();
let products = ref(null);

onBeforeMount(async () => {
  try {
    const response = await fetch("https://api.escuelajs.co/api/v1/products");
    if (response.status === 200) {
      const data = await response.json();
      products.value = data;
      setTimeout(() => (userStore.isLoading  = false), 1000);
    } else {
      console.log("Error: Unable to fetch data");
      userStore.isLoading  = false;
    }
  } catch (error) {
    console.error(error);
    userStore.isLoading  = false;
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