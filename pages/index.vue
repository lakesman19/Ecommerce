<template>
  <MainLayouts>
    <div id="IndexPage" class="mt-4 max-w-[1200px] mx-auto px-2">
      <div
        class="grid xl:grid-cols-6 lg:grid-cols-5 md:grid-cols-4 sm:grid-cols-3 grid-cols-2 gap-4"
      >
        <div v-if="products" v-for="product in products.data" :key="product">
          <ProductComponent :product="product" />
        </div>
      </div>
      index
    </div></MainLayouts
  >
</template>

<script setup>
import MainLayouts from "~/layouts/MainLayouts.vue";


const products =[{}]
</script>

