
<template>
  <MainLayouts>
    <div id="AddressPage" class="mt-4 max-w-[500px] mx-auto px-2">
      <div class="mx-auto bg-white rounded-lg p-3">
        <div class="text-xl text-bold mb-2">Address Details</div>
        <form action="">
          <TextInputs
            class="w-full"
            placeholder="Contact Name"
            v-model:input="contactName"
            inputType="text"
            :error="error && error.type == 'contactName' ? error.message : ''"
          />

          <TextInputs
            class="w-full mt-2"
            placeholder="Address"
            v-model:input="address"
            inputType="text"
            :error="error && error.type == 'address' ? error.message : ''"
          />

          <TextInputs
            class="w-full mt-2"
            placeholder="Zip Code"
            v-model:input="zipCode"
            inputType="text"
            :error="error && error.type == 'zipCode' ? error.message : ''"
          />

          <TextInputs
            class="w-full mt-2"
            placeholder="City"
            v-model:input="city"
            inputType="text"
            :error="error && error.type == 'city' ? error.message : ''"
          />

          <TextInputs
            class="w-full mt-2"
            placeholder="Country"
            v-model:input="country"
            inputType="text"
            :error="error && error.type == 'country' ? error.message : ''"
          />

          <button
            :disabled="isWorking"
            type="submit"
            class="mt-6 bg-gradient-to-r from-[#FE630C] to-[#FF3200] w-full text-white text-[21px] font-semibold p-1.5 rounded-full"
          >
            <div v-if="true">Update Address</div>
            <Icon v-else name="eos-icons:loading" size="25" class="mr-2" />
          </button>
        </form>
      </div>
    </div>
  </MainLayouts>
</template>

<script setup>
import MainLayouts from "~/layouts/MainLayouts.vue";
import TextInputs from "~/components/TextInputs.vue";
// import Inputs from "~/components/Inputs.vue";
import { useUserStore } from "~/stores/user";
const userStore = useUserStore();
let contactName = ref(null);
let address = ref(null);
let zipCode = ref(null);
let city = ref(null);
let country = ref(null);
</script>

<style lang="scss" scoped>
</style>

