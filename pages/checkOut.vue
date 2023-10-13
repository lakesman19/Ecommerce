
<template>
  <MainLayouts>
    <div id="CheckoutPage" class="mt-4 max-w-[1200px] mx-auto px-2">
      <div class="md:flex gap-4 justify-between mx-auto w-full">
        <div class="md:w-[65%]">
          <div class="bg-white rounded-lg p-4">
            <div class="text-xl font-semibold mb-2">Shipping Address</div>

            <div v-if="currentAddress && currentAddress.data">
              <NuxtLink
                to="/address"
                class="flex items-center pb-2 text-blue-500 hover:text-red-400"
              >
                <Icon name="mdi:plus" size="18" class="mr-2" />
                Update Address
              </NuxtLink>

              <div class="pt-2 border-t">
                <div class="underline pb-1">Delivery Address</div>
                <ul class="text-xs">
                  <li class="flex items-center gap-2">
                    <div>Contact name:</div>
                    <div class="font-bold">{{ currentAddress.data.name }}</div>
                  </li>
                  <li class="flex items-center gap-2">
                    <div>Address:</div>
                    <div class="font-bold">
                      {{ currentAddress.data.address }}
                    </div>
                  </li>
                  <li class="flex items-center gap-2">
                    <div>Zip Code:</div>
                    <div class="font-bold">
                      {{ currentAddress.data.zipcode }}
                    </div>
                  </li>
                  <li class="flex items-center gap-2">
                    <div>City:</div>
                    <div class="font-bold">{{ currentAddress.data.city }}</div>
                  </li>
                  <li class="flex items-center gap-2">
                    <div>Country:</div>
                    <div class="font-bold">
                      {{ currentAddress.data.country }}
                    </div>
                  </li>
                </ul>
              </div>
            </div>

            <NuxtLink
              v-else
              to="/address"
              class="flex items-center text-blue-500 hover:text-red-400"
            >
              <Icon name="mdi:plus" size="18" class="mr-2" />
              Add New Address
            </NuxtLink>
          </div>

          <div id="Items" class="bg-white rounded-lg p-4 mt-4">
            <div v-for="product in userStore.checkout" :key="product">
              <CheckOutItem :product="product" />
            </div>
          </div>
        </div>

        <div class="md:hidden block my-4" />
        <div class="md:w-[35%]">
          <div id="PlaceOrder" class="bg-white rounded-lg p-4">
            <div class="text-2xl font-extrabold mb-2">Summary</div>

            <div class="flex items-center justify-between my-4">
              <div class="">Total Shipping</div>
              <div class="">Free</div>
            </div>

            <div class="border-t" />

            <div class="flex items-center justify-between my-4">
              <div class="font-semibold">Total</div>
              <div class="text-2xl font-semibold">
                $ <span class="font-extrabold">{{ total / 10 }}</span>
              </div>
            </div>

            <form @submit.prevent="pay()">
              <div
                class="border border-gray-500 p-2 rounded-sm"
                id="card-element"
              />

              <p
                id="card-error"
                role="alert"
                class="text-red-700 text-center font-semibold"
              />

              <button
                :disabled="isProcessing"
                type="submit"
                class="mt-4 bg-gradient-to-r from-[#FE630C] to-[#FF3200] w-full text-white text-[21px] font-semibold p-1.5 rounded-full"
                :class="isProcessing ? 'opacity-70' : 'opacity-100'"
              >
                <Icon v-if="isProcessing" name="eos-icons:loading" />
                <div v-else>Place order</div>
              </button>
            </form>
          </div>

          <div class="bg-white rounded-lg p-4 mt-4">
            <div class="text-lg font-semibold mb-2 mt-2">AliExpress</div>
            <p class="my-2">
              AliExpress keeps your information and payment safe
            </p>
          </div>
        </div>
      </div>
    </div>
  </MainLayouts>
</template>


<script setup>
import MainLayouts from "~/layouts/MainLayouts.vue";
import CheckOutItem from "~/components/CheckOutItem.vue";
import { useUserStore } from "~/stores/user";
const userStore = useUserStore();

const route = useRoute();
const products = [
  {
    id: 1,
    title: "1",
    description: "This is a description",
    url: "https://piscum.photos/id/7/800/800",
    price: 999,
  },
  {
    id: 2,
    title: "2",
    description: "This is a description",
    url: "https://piscum.photos/id/71/800/800",
    price: 999,
  },
  {
    id: 3,
    title: "3",
    description: "This is a description",
    url: "https://piscum.photos/id/72/800/800",
    price: 999,
  },
  {
    id: 4,
    title: "4",
    description: "This is a description",
    url: "https://piscum.photos/id/73/800/800",
    price: 999,
  },
  {
    id: 5,
    title: "5",
    description: "This is a description",
    url: "https://piscum.photos/id/74/800/800",
    price: 999,
  },
  {
    id: 6,
    title: "6",
    description: "This is a description",
    url: "https://piscum.photos/id/75/800/800",
    price: 999,
  },
  {
    id: 7,
    title: "7",
    description: "This is a description",
    url: "https://piscum.photos/id/76/800/800",
    price: 999,
  },
  {
    id: 8,
    title: "8",
    description: "This is a description",
    url: "https://piscum.photos/id/77/800/800",
    price: 999,
  },
  {
    id: 9,
    title: "9",
    description: "This is a description",
    url: "https://piscum.photos/id/78/800/800",
    price: 999,
  },
  {
    id: 10,
    title: "10",
    description: "This is a description",
    url: "https://piscum.photos/id/79/800/800",
    price: 999,
  },
];

let total = ref(0);

let isProcessing = ref(false);

onBeforeMount(async () => {
  if (userStore.checkout.length < 1) {
    return navigateTo("/shoppingCart");
  }

  total.value = 0.0;
});
onMounted(async () => {
  isProcessing.value = false;

  userStore.checkout.forEach((item) => {
    total.value += item.price;
  });
});
// watch(
//   () => total.value,
//   () => {
//     if (total.value > 0) {
//       // stripeInit();
//     }
//   }
// );
const pay = () => {
  setTimeout(() => {
    isProcessing.value = false;
    userStore.cart = [];
    userStore.checkout = [];
    return navigateTo("/success");
  }, 500);
};
</script> 