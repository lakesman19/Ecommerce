<template>
  <MainLayouts>
    <div id="ShoppingCartPage" class="mt-4 max-w-[1200px] mx-auto px-2">
      <div v-if="true" class="h-[500px] flex items-center justify-center">
        <div class="pt-20">
          <img class="mx-auto" width="250" src="../public/cart-empty (2).png" />
          <div class="text-xl text-center mt-4">No items yet?</div>
          <div class="text-xl text-center mt-4">No items yet?</div>

          <div v-if="true" class="flex text-center">
            <NuxtLink
              to="/auth"
              class="bg-[#FD374F] w-full text-white text-[21px] font-semibold p-1.5 rounded-full mt-4"
            >
              Sign in
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </MainLayouts>
</template>

<script setup>
import MainLayouts from "~/layouts/MainLayouts.vue";
</script>

