<template>
  <div class="py-3">
    <div class="continue flex justify-center mt-3 mb-3 items-center">
      <button
        @click="toggleContent"
        class="w-[370px] h-[48px] flex items-center justify-center bg-[#0078FF] text-white font-bold py-4 px-4 rounded-[10px] hover:bg-[#0078FF] transition"
      >
        Continue
      </button>
    </div>
    <!-- Animated Content -->
    <transition name="slide-up">

    <div   v-if="showContent"
      class="text-arrow bg-slate-100 py-3 px-4 min-h-screen max-w-md mx-auto"
    >
      <h1 class="font-[700] text-[18px] text-[#273443]">Your Plan</h1>
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
            <span class="font-bold">$108.00</span>
            <span class="text-gray-500">-$54.00</span>
          </div>
        </div>
        <div class="border mt-3"></div>
        <div class="flex justify-between items-center mt-3">
          <h1 class="font-bold text-[18px]">Total</h1>
          <span class="font-bold text-blue-600 text-[18px]">$54.00</span>
        </div>
      </div>
      <!-- ///create btn-pay////// -->
      <div class="flex justify-center items-center mt-4">
        <button
          class="flex justify-center items-center bg-black w-[450px] py-1 px-2 h-[52px] rounded-[18px]"
        >
          <img
            src="../assets/apple-pay-brands-solid.svg"
            alt="pay"
            class="w-16 m-auto"
          />
        </button>
      </div>
     <!-- Divider with "or" -->
        <div class="flex items-center justify-center mt-4">
          <hr class="border w-full max-w-[160px]" />
          <span class="px-2 text-gray-500 font-bold">or</span>
          <hr class="border w-full max-w-[160px]" />
        </div>
      <!-- ///create btn-pay////// -->
      <div class="max-w-md mx-auto p-6 bg-[#DCEDFF] rounded-lg mt-3">
        <h2
          class="text-lg font-bold mb-4 flex items-center gap-2 justify-center text-[#0078FF]"
        >
          Pay with Credit Card
        </h2>
        <form @submit.prevent="handleSubmit">
          <!-- Card Number -->
          <div class="mb-4">
            <label
              for="card-number"
              class="block font-normal text-[16px] text-[#101F29]"
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
              <label
                for="exp-date"
                class="block font-normal text-[16px] text-[#101F29]"
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
              <label
                for="cvc"
                class="block font-normal text-[16px] text-[#101F29]"
                >CVC</label
              >
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
            <label
              for="cardholder-name"
              class="block font-normal text-[16px] text-[#101F29]"
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
            <label
              for="country"
              class="block font-normal text-[16px] text-[#101F29]"
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
            class="w-full bg-[#8D8D91] text-white font-bold py-4 px-4 rounded hover:bg-[#8D8D91] transition"
          >
            Subscribe
          </button>
          <div class="flex justify-center gap-2 mt-3">
            <svg
              width="29"
              height="20"
              viewBox="0 0 29 20"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M25.7003 19.9998H3.11348C1.39398 19.9998 0 18.5485 0 16.7582V3.24163C0 1.45136 1.39398 0 3.11348 0H25.7003C27.4199 0 28.8138 1.45136 28.8138 3.24163V16.7581C28.8138 18.5485 27.4198 19.9998 25.7003 19.9998Z"
                fill="#E8E9EB"
              />
              <path
                d="M8.47653 17.2576V16.3386C8.47653 15.9871 8.25019 15.757 7.86164 15.757C7.66737 15.757 7.45612 15.8176 7.31088 16.0175C7.19771 15.8497 7.0355 15.757 6.79219 15.757C6.62998 15.757 6.46777 15.8033 6.33951 15.9711V15.7873H6V17.2576H6.33951V16.4457C6.33951 16.1852 6.48474 16.0621 6.71108 16.0621C6.93742 16.0621 7.05059 16.1995 7.05059 16.4457V17.2576H7.3901V16.4457C7.3901 16.1852 7.55231 16.0621 7.76168 16.0621C7.98802 16.0621 8.10119 16.1995 8.10119 16.4457V17.2576H8.47653ZM13.5126 15.7873H12.9618V15.343H12.6223V15.7873H12.3149V16.0781H12.6223V16.7526C12.6223 17.0899 12.7676 17.2879 13.1561 17.2879C13.3013 17.2879 13.4636 17.2415 13.5767 17.1809L13.4786 16.9043C13.3806 16.965 13.2674 16.981 13.1863 16.981C13.0241 16.981 12.9599 16.8882 12.9599 16.7366V16.0781H13.5107V15.7873H13.5126ZM16.3947 15.7552C16.2004 15.7552 16.0702 15.848 15.9891 15.9693V15.7855H15.6496V17.2558H15.9891V16.4279C15.9891 16.1834 16.1023 16.0442 16.3135 16.0442C16.3777 16.0442 16.4588 16.0603 16.5248 16.0746L16.6229 15.7677C16.555 15.7552 16.4588 15.7552 16.3947 15.7552ZM12.0395 15.9086C11.8773 15.8016 11.6509 15.7552 11.4076 15.7552C11.0191 15.7552 10.7607 15.939 10.7607 16.2298C10.7607 16.4743 10.955 16.6134 11.2945 16.658L11.4567 16.6741C11.634 16.7044 11.7321 16.7508 11.7321 16.8276C11.7321 16.9346 11.6019 17.0113 11.3756 17.0113C11.1492 17.0113 10.97 16.9346 10.8569 16.8579L10.6947 17.1023C10.872 17.2255 11.1153 17.2861 11.3586 17.2861C11.8113 17.2861 12.0716 17.0863 12.0716 16.8115C12.0716 16.551 11.8603 16.4136 11.5378 16.3672L11.3756 16.3511C11.2303 16.3351 11.1172 16.3047 11.1172 16.2137C11.1172 16.1067 11.2303 16.046 11.4095 16.046C11.6038 16.046 11.7981 16.1227 11.8962 16.1691L12.0395 15.9086ZM21.0723 15.7552C20.8781 15.7552 20.7479 15.848 20.6668 15.9693V15.7855H20.3273V17.2558H20.6668V16.4279C20.6668 16.1834 20.78 16.0442 20.9912 16.0442C21.0554 16.0442 21.1365 16.0603 21.2025 16.0746L21.3006 15.7712C21.2346 15.7552 21.1384 15.7552 21.0723 15.7552ZM16.7342 16.5224C16.7342 16.9667 17.0586 17.2879 17.5603 17.2879C17.7866 17.2879 17.9489 17.2415 18.1111 17.1202L17.9489 16.8597C17.8187 16.9525 17.6904 16.9971 17.5433 16.9971C17.2679 16.9971 17.0737 16.8133 17.0737 16.5224C17.0737 16.2459 17.2679 16.0621 17.5433 16.0478C17.6886 16.0478 17.8187 16.0942 17.9489 16.1852L18.1111 15.9247C17.9489 15.8016 17.7866 15.757 17.5603 15.757C17.0586 15.7552 16.7342 16.0781 16.7342 16.5224ZM19.8746 16.5224V15.7873H19.5351V15.9711C19.4219 15.8337 19.2597 15.757 19.0485 15.757C18.6109 15.757 18.2714 16.0781 18.2714 16.5224C18.2714 16.9667 18.6109 17.2879 19.0485 17.2879C19.2748 17.2879 19.437 17.2112 19.5351 17.0738V17.2576H19.8746V16.5224ZM18.6279 16.5224C18.6279 16.2619 18.8052 16.0478 19.0975 16.0478C19.3729 16.0478 19.5672 16.2476 19.5672 16.5224C19.5672 16.7829 19.3729 16.9971 19.0975 16.9971C18.8071 16.981 18.6279 16.7812 18.6279 16.5224ZM14.5651 15.7552C14.1124 15.7552 13.788 16.0621 13.788 16.5207C13.788 16.981 14.1124 17.2861 14.582 17.2861C14.8084 17.2861 15.0347 17.2255 15.2139 17.0863L15.0517 16.8561C14.9216 16.9489 14.7593 17.0096 14.599 17.0096C14.3878 17.0096 14.1784 16.9168 14.1294 16.658H15.278C15.278 16.6117 15.278 16.5813 15.278 16.5349C15.2931 16.0621 15.0008 15.7552 14.5651 15.7552ZM14.5651 16.0317C14.7763 16.0317 14.9216 16.1549 14.9536 16.3833H14.1445C14.1765 16.1852 14.3218 16.0317 14.5651 16.0317ZM23 16.5224V15.2056H22.6605V15.9711C22.5473 15.8337 22.3851 15.757 22.1739 15.757C21.7363 15.757 21.3968 16.0781 21.3968 16.5224C21.3968 16.9667 21.7363 17.2879 22.1739 17.2879C22.4002 17.2879 22.5624 17.2112 22.6605 17.0738V17.2576H23V16.5224ZM21.7532 16.5224C21.7532 16.2619 21.9305 16.0478 22.2229 16.0478C22.4983 16.0478 22.6926 16.2476 22.6926 16.5224C22.6926 16.7829 22.4983 16.9971 22.2229 16.9971C21.9305 16.981 21.7532 16.7812 21.7532 16.5224ZM10.3872 16.5224V15.7873H10.0477V15.9711C9.93454 15.8337 9.77233 15.757 9.56108 15.757C9.12349 15.757 8.78398 16.0781 8.78398 16.5224C8.78398 16.9667 9.12349 17.2879 9.56108 17.2879C9.78742 17.2879 9.94963 17.2112 10.0477 17.0738V17.2576H10.3872V16.5224ZM9.12537 16.5224C9.12537 16.2619 9.30267 16.0478 9.59503 16.0478C9.87041 16.0478 10.0647 16.2476 10.0647 16.5224C10.0647 16.7829 9.87041 16.9971 9.59503 16.9971C9.30267 16.981 9.12537 16.7812 9.12537 16.5224Z"
                fill="#121212"
              />
              <path
                d="M16.7985 3.95346H11.9202V13.0786H16.7985V3.95346Z"
                fill="#FF5A00"
              />
              <path
                d="M12.2455 8.51635C12.2455 6.6624 13.0826 5.01695 14.3671 3.95379C13.4218 3.1799 12.2292 2.71219 10.9285 2.71219C7.84704 2.71219 5.35376 5.3081 5.35376 8.51635C5.35376 11.7246 7.84704 14.3205 10.9285 14.3205C12.2292 14.3205 13.4218 13.8528 14.3671 13.0789C13.0808 12.0308 12.2455 10.3703 12.2455 8.51635Z"
                fill="#EB001B"
              />
              <path
                d="M23.3812 8.51635C23.3812 11.7246 20.8879 14.3205 17.8065 14.3205C16.5057 14.3205 15.3132 13.8528 14.3679 13.0789C15.6686 12.0139 16.4895 10.3703 16.4895 8.51635C16.4895 6.6624 15.6524 5.01695 14.3679 3.95379C15.3114 3.1799 16.5039 2.71219 17.8047 2.71219C20.8879 2.71219 23.3812 5.325 23.3812 8.51635Z"
                fill="#F79E1B"
              />
            </svg>
            <svg
              width="32"
              height="20"
              viewBox="0 0 32 20"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M25.3709 8.29564C25.3608 8.24401 25.2696 8.29329 25.2524 8.34298C25.2318 8.40252 24.8667 9.44667 24.8457 9.50608C24.681 9.97286 24.4594 10.6003 24.323 10.9847C24.2824 11.0991 24.3672 11.2192 24.4885 11.2192H25.585C25.7739 11.2192 25.9158 11.0472 25.879 10.8619C25.7387 10.1549 25.4746 8.82982 25.4729 8.82135C25.4728 8.82103 25.4728 8.82115 25.4728 8.82083L25.3709 8.29564Z"
                fill="#002CF0"
              />
              <path
                d="M4.3 0C1.92518 0 0 1.92518 0 4.3V15.6998C0 18.0747 1.92518 19.9998 4.3 19.9998H27.3286C29.7034 19.9998 31.6286 18.0747 31.6286 15.6998V4.3C31.6286 1.92518 29.7034 0 27.3286 0H4.3ZM7.3057 14.1576C7.16846 14.1576 7.04871 14.0645 7.01494 13.9315L5.45141 7.7733C5.43486 7.70814 5.39691 7.65042 5.34364 7.60941L3.77443 6.40136C3.5475 6.22665 3.67104 5.86364 3.95744 5.86364H6.97964C7.12382 5.86364 7.24761 5.96621 7.27441 6.10788L8.09306 10.4358C8.14995 10.7365 8.56779 10.769 8.67045 10.4807L10.2433 6.06323C10.2858 5.94369 10.399 5.86386 10.5259 5.86386H12.058C12.2692 5.86386 12.4143 6.07641 12.3373 6.27315L9.32753 13.967C9.28254 14.082 9.17165 14.1577 9.04814 14.1577L7.3057 14.1576ZM14.1423 13.9101C14.1196 14.0563 13.9938 14.1641 13.8458 14.1641H12.3928C12.2088 14.1641 12.0681 14 12.0963 13.8181L13.2922 6.11113C13.3149 5.96495 13.4407 5.85713 13.5887 5.85713H15.0416C15.2256 5.85713 15.3663 6.02128 15.338 6.20312L14.1423 13.9101ZM17.6896 14.2877C16.8835 14.2785 16.1036 14.1247 15.5984 13.9321C15.475 13.8851 15.4078 13.7557 15.4281 13.6251L15.6368 12.2784C15.6592 12.1335 15.8162 12.0523 15.9474 12.1177C16.6249 12.4278 17.0632 12.5535 17.888 12.5535C18.4805 12.5535 19.1157 12.2984 19.121 11.742C19.1245 11.3784 18.8547 11.118 18.0518 10.7112C17.2709 10.3147 16.2346 9.6481 16.2471 8.45436C16.2595 6.83976 17.6934 5.7123 19.7303 5.7123C20.3958 5.7123 20.9524 5.83896 21.3551 5.97777C21.4863 6.02299 21.5614 6.15772 21.5402 6.29485L21.3296 7.65616C21.3139 7.75736 21.2038 7.81354 21.1127 7.7668C20.732 7.5981 20.2448 7.43619 19.5705 7.4477C18.7635 7.4477 18.3907 7.81725 18.3902 8.16233C18.3851 8.55243 18.8272 8.80755 19.5471 9.19301C20.7361 9.78569 21.2849 10.5032 21.2777 11.4502C21.2614 13.1738 19.8547 14.2877 17.6896 14.2877ZM26.7825 14.1674C26.6394 14.1674 26.5162 14.0665 26.4882 13.9261C26.4455 13.7115 26.3824 13.3963 26.3344 13.1608C26.3061 13.022 26.1846 12.923 26.043 12.9228C25.5099 12.9219 24.3527 12.9193 23.8576 12.9185C23.7306 12.9183 23.6185 12.9981 23.5767 13.118C23.4914 13.3628 23.3624 13.7362 23.2833 13.9653C23.2415 14.0863 23.1276 14.1675 22.9996 14.1675H21.4931C21.2806 14.1675 21.1355 13.9527 21.2147 13.7556L24.1093 6.55417C24.3252 6.01266 24.6953 5.86559 25.1892 5.86559H26.5354C26.6783 5.86559 26.8014 5.96641 26.8295 6.10653L28.3763 13.8084C28.4136 13.9942 28.2716 14.1675 28.0822 14.1675L26.7825 14.1674Z"
                fill="#002CF0"
              />
            </svg>
          </div>
        </form>
      </div>
    </div>
    </transition>
  </div>
</template>
<script>
export default {
  data() {
    return {
          showContent: false, // Toggle content visibility

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
    toggleContent() {
      this.showContent = !this.showContent;
    },
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

<style scoped>
/* Animation for sliding up */
.slide-up-enter-active,
.slide-up-leave-active {
  transition: all 0.5s ease;
}
.slide-up-enter-from,
.slide-up-leave-to {
  transform: translateY(100%);
  opacity: 0;
}
</style>
