<template>
  <div class="py-3">
    <div
      class="content flex justify-start bg-white max-w-md mx-auto rounded-t-lg shadow py-5 px-3"
    >
      <div class="img-user">
        <div class="flex gap-3 items-center">
          <img src="../assets/logo.png" alt="logo" class="w-[50px] rounded-[4px]" />
          <h1 class="text-blue-600 font-bold">
            Hi, Khaled <br />
            <p class="text-black font-normal">Freemium</p>
          </h1>
        </div>
      </div>
    </div>
    <div
      class="text-arrow bg-slate-100 py-3 px-4 min-h-screen max-w-md mx-auto"
    >
      <div class="icon w-[15px] mb-2">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
          <!--!Font Awesome Free 6.7.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.-->
          <path
            d="M9.4 233.4c-12.5 12.5-12.5 32.8 0 45.3l160 160c12.5 12.5 32.8 12.5 45.3 0s12.5-32.8 0-45.3L109.2 288 416 288c17.7 0 32-14.3 32-32s-14.3-32-32-32l-306.7 0L214.6 118.6c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0l-160 160z"
          />
        </svg>
      </div>
      <h1 class="font-bold">Your Plan</h1>
      <div class="bg-white py-2 px-3 rounded-[4px] mt-3 max-w-md mx-auto">
        <div class="flex justify-between items-center">
          <div class="flex flex-col">
            <div class="px-2">One Year</div>
            <div class="mt-2 flex items-center gap-2">
              <img
                src="../assets/Screenshot 2024-12-07 180102.png"
                alt="icon"
                class="w-[25px]"
              />
              <h1 class="text-blue-600 font-bold">FRIDAY</h1>
              <p class="text-gray-500 font-bold">(40%off)</p>
            </div>
          </div>
          <div class="flex flex-col items-center">
            <span>$59.99</span>
            <span class="text-gray-500">-$20.00</span>
          </div>
        </div>
        <div class="border mt-3"></div>
        <div class="flex justify-between items-center mt-3">
          <h1 class="font-bold text-[18px]">Total</h1>
          <span class="font-bold text-blue-600 text-[18px]">$39.99</span>
        </div>
      </div>
      <!-- ///create btn-pay////// -->
      <div class="flex justify-center items-center mt-4">
        <button
          class="flex justify-center items-center bg-black w-[450px] py-1 px-2 h-[55px] rounded-[18px]"
        >
          <img
            src="../assets/apple-pay-brands-solid.svg"
            alt="pay"
            class="w-16 m-auto"
          />
        </button>
      </div>
      <!-- ///create btn-pay////// -->
      <div class="max-w-md mx-auto p-6 bg-white rounded-lg mt-3">
        <h2 class="text-lg font-bold mb-4 flex items-center gap-2">
          Credit Card
          <img src="../assets/masicon.png" alt="MasterCard" class="h-5" />
          <img src="../assets/visa.png" alt="Visa" class="h-5" />
        </h2>
        <form @submit.prevent="handleSubmit">
          <!-- Card Number -->
          <div class="mb-4">
            <label for="card-number" class="block font-normal text-[18px]"
              >Card number</label
            >
            <input
              type="text"
              id="card-number"
              v-model="formData.cardNumber"
              placeholder=""
              name="Card number"
              class="mt-1 block w-full p-[10px] border-none bg-gray-50 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500"
            />
            <p v-if="errors.cardNumber" class="text-red-500 text-sm">
              {{ errors.cardNumber }}
            </p>
          </div>

          <!-- Expiry Date and CVC -->
          <div class="mb-4 flex gap-4">
            <div class="flex-1">
              <label for="exp-date" class="block font-normal text-[18px]"
                >Exp. Date</label
              >
              <input
                type="text"
                id="exp-date"
                v-model="formData.expDate"
                placeholder=""
                name="Exp. Date"
                class="mt-1 block w-full p-2 border-none bg-gray-50 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500"
              />
              <p v-if="errors.expDate" class="text-red-500 text-sm">
                {{ errors.expDate }}
              </p>
            </div>
            <div class="flex-1">
              <label for="cvc" class="block font-normal text-[18px]">CVC</label>
              <input
                type="text"
                id="cvc"
                v-model="formData.cvc"
                name="CVC"
                placeholder=""
                class="mt-1 block w-full p-2 border-none bg-gray-50 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500"
              />
              <p v-if="errors.cvc" class="text-red-500 text-sm">
                {{ errors.cvc }}
              </p>
            </div>
          </div>

          <!-- Cardholder Name -->
          <div class="mb-4">
            <label for="cardholder-name" class="block font-normal text-[18px]"
              >Cardholder name</label
            >
            <input
              type="text"
              id="cardholder-name"
              v-model="formData.cardholderName"
              placeholder=""
              name="Cardholder"
              class="mt-1 block w-full p-2 border-none bg-gray-50 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500"
            />
            <p v-if="errors.cardholderName" class="text-red-500 text-sm">
              {{ errors.cardholderName }}
            </p>
          </div>

          <!-- Country -->
          <div class="mb-6">
            <label for="country" class="block font-normal text-[18px]"
              >Country</label
            >
            <select
              id="country"
              v-model="formData.country"
              class="mt-1 block w-full p-[10px] border-none bg-gray-50 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500"
            >
              <option value=""></option>
              <option value="us">United States</option>
              <option value="uk">United Kingdom</option>
              <option value="ca">Canada</option>
              <!-- Add more options as needed -->
            </select>
            <p v-if="errors.country" class="text-red-500 text-sm">
              {{ errors.country }}
            </p>
          </div>

          <!-- Submit Button -->
          <button
            type="submit"
            class="w-full bg-[#8d8d91] text-white font-bold py-4 px-4 rounded hover:bg-[#8d8d91] transition"
          >
            Subscribe
          </button>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      // Form data
      formData: {
        cardNumber: "",
        expDate: "",
        cvc: "",
        cardholderName: "",
        country: "",
      },
      // Validation errors
      errors: {},
    };
  },
  methods: {
    // Handle form submission
    handleSubmit() {
      this.errors = {}; // Reset errors
      let valid = true;

      // Validate each field
      if (!this.formData.cardNumber) {
        this.errors.cardNumber = "Card number is required";
        valid = false;
      }
      if (!this.formData.expDate) {
        this.errors.expDate = "Expiration date is required";
        valid = false;
      }
      if (!this.formData.cvc) {
        this.errors.cvc = "CVC is required";
        valid = false;
      }
      if (!this.formData.cardholderName) {
        this.errors.cardholderName = "Cardholder name is required";
        valid = false;
      }
      if (!this.formData.country) {
        this.errors.country = "Country is required";
        valid = false;
      }

      if (valid) {
        alert("Form submitted successfully!");
        console.log(this.formData);
      } else {
        alert("Please fix the errors before submitting.");
      }
    },
  },
};
</script>

<style scoped></style>
