<template>
  <div class="pt-[150px] relative">
    <p
      @click="showCreateWallet = !showCreateWallet"
      class="bg-[#1D2633] w-[30px] h-[30px] text-center rounded-full cursor-pointer hover:bg-[#313c4a] top-[30px] absolute left-[20px]"
    >
      <router-link to="/settings">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="1rem"
          height="1rem"
          class="ml-[7px] mt-[7px]"
          viewBox="0 0 16 16"
        >
          <path
            d="M10.3075 3.50173C10.5846 3.19385 10.5596 2.71963 10.2517 2.44254C9.94384 2.16544 9.46962 2.1904 9.19253 2.49828L4.69253 7.49828C4.43582 7.78351 4.43582 8.2165 4.69253 8.50173L9.19253 13.5017C9.46962 13.8096 9.94384 13.8346 10.2517 13.5575C10.5596 13.2804 10.5846 12.8062 10.3075 12.4983L6.25902 8.00001L10.3075 3.50173Z"
            fill="currentColor"
          />
        </svg>
      </router-link>
    </p>
    <h1 class="font-bold text-[24px] text-center">Your recovery phrase</h1>
    <p class="gr text-center">
      Write down these 12 words in the order given below and store them
      in a secret, safe place.
    </p>
    <div class="c">
      <span v-for="(phrase, index) in randomPh" class="text-[16px] ml-[15px]">
        <span class="gr mr-[10px]">{{ index + 1 }}</span> {{ phrase }}
      </span>
    </div>
  </div>
  <div
    class="flex justify-evenly fixed bottom-0 w-[530px] bg-[#0B0F16] pb-[10px]"
  >
    <router-link to="/wallet">
      <div class="">
        <svg
          class="ml-[5px]"
          xmlns="http://www.w3.org/2000/svg"
          width="29"
          height="28"
          viewBox="0 0 29 28"
        >
          <path
            opacity="0.32"
            d="M3.75 9.4C3.75 7.15979 3.75 6.03968 4.18597 5.18404C4.56947 4.43139 5.18139 3.81947 5.93404 3.43597C6.78968 3 7.90979 3 10.15 3H16.35C18.5902 3 19.7103 3 20.566 3.43597C21.3186 3.81947 21.9305 4.43139 22.314 5.18404C22.75 6.03968 22.75 7.15979 22.75 9.4V12H3.75V9.4Z"
            fill="#8994A3"
          />
          <path
            opacity="0.32"
            d="M18.75 12.5H22.75V16.5H18.75V12.5Z"
            fill="#8994A3"
          />
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M4.18597 8.18404C3.75 9.03969 3.75 10.1598 3.75 12.4V16.6C3.75 18.8402 3.75 19.9603 4.18597 20.816C4.56947 21.5686 5.18139 22.1805 5.93404 22.564C6.78969 23 7.90979 23 10.15 23H19.35C21.5902 23 22.7103 23 23.566 22.564C24.3186 22.1805 24.9305 21.5686 25.314 20.816C25.75 19.9603 25.75 18.8402 25.75 16.6V12.4C25.75 10.1598 25.75 9.03969 25.314 8.18404C24.9305 7.43139 24.3186 6.81947 23.566 6.43597C22.7103 6 21.5902 6 19.35 6H10.15C7.90979 6 6.78969 6 5.93404 6.43597C5.18139 6.81947 4.56947 7.43139 4.18597 8.18404ZM20.5 12.75C19.5335 12.75 18.75 13.5335 18.75 14.5C18.75 15.4665 19.5335 16.25 20.5 16.25C21.4665 16.25 22.25 15.4665 22.25 14.5C22.25 13.5335 21.4665 12.75 20.5 12.75Z"
            fill="#8994A3"
          />
        </svg>
        <p class="text-[12px] font-bold text-[#8994A3]">Wallet</p>
      </div>
    </router-link>
    <router-link to="/history">
      <div class="">
        <svg
          class="ml-[5px]"
          xmlns="http://www.w3.org/2000/svg"
          width="29"
          height="28"
          viewBox="0 0 29 28"
        >
          <path
            opacity="0.32"
            d="M11.7694 14.6521L10.8499 21.6403C10.596 23.5702 10.469 24.5352 10.6533 25.0115C11.0322 25.9906 12.1037 26.51 13.107 26.2011C13.5952 26.0508 14.2741 25.3535 15.6321 23.9589L22.4646 16.9417C23.8441 15.5249 24.5338 14.8165 24.7122 14.2471C25.0774 13.0808 24.5459 11.8214 23.4554 11.2695C22.9231 11 21.9344 11 19.957 11H15.9335C14.9419 11 14.4461 11 14.029 11.1236C13.1874 11.3728 12.4973 11.9781 12.1404 12.7799C11.9634 13.1774 11.8988 13.6689 11.7694 14.6521Z"
            fill="#8994A3"
          />
          <path
            d="M16.7305 13.3479L17.6499 6.35974C17.9039 4.42981 18.0309 3.46485 17.8465 2.98851C17.4676 2.00944 16.3962 1.48997 15.3928 1.79887C14.9047 1.94915 14.2257 2.64649 12.8678 4.04114L6.03521 11.0583C4.65575 12.4751 3.96602 13.1835 3.7877 13.7529C3.42245 14.9192 3.95398 16.1786 5.04441 16.7305C5.57677 17 6.56547 17 8.54286 17H12.5663C13.558 17 14.0538 17 14.4709 16.8765C15.3124 16.6272 16.0026 16.0219 16.3595 15.2201C16.5364 14.8227 16.6011 14.3311 16.7305 13.3479Z"
            fill="#8994A3"
          />
        </svg>
        <p class="text-[12px] font-bold text-[#8994A3]">History</p>
      </div>
    </router-link>
    <router-link to="/setting">
      <div class="">
        <svg
          class="ml-[10px]"
          xmlns="http://www.w3.org/2000/svg"
          width="29"
          height="28"
          viewBox="0 0 29 28"
        >
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M11.9386 3.50061L16.5641 3.50061C17.9312 3.49781 18.6147 3.49641 19.2265 3.69463C19.7678 3.87001 20.266 4.15763 20.6885 4.5387C21.166 4.9694 21.5066 5.56208 22.1877 6.74744L24.5005 10.7532C25.1864 11.9357 25.5294 12.527 25.6636 13.1559C25.7824 13.7124 25.7824 14.2876 25.6636 14.8441C25.5294 15.473 25.1864 16.0642 24.5005 17.2467L22.1877 21.2526C21.5066 22.4379 21.166 23.0306 20.6885 23.4613C20.266 23.8424 19.7678 24.13 19.2265 24.3054C18.6147 24.5036 17.9312 24.5022 16.5641 24.4994H11.9386C10.5715 24.5022 9.88798 24.5036 9.2762 24.3054C8.73492 24.13 8.23674 23.8424 7.81422 23.4613C7.33667 23.0306 6.9961 22.4379 6.31497 21.2526L4.00226 17.2468C3.31628 16.0643 2.97329 15.473 2.83907 14.8441C2.72031 14.2876 2.72031 13.7124 2.83907 13.1559C2.97329 12.527 3.31628 11.9357 4.00226 10.7532L6.31497 6.74744C6.9961 5.56208 7.33667 4.96941 7.81422 4.53871C8.23674 4.15763 8.73492 3.87001 9.2762 3.69463C9.88798 3.49641 10.5715 3.49781 11.9386 3.50061ZM14.25 18C16.4591 18 18.25 16.2091 18.25 14C18.25 11.7909 16.4591 10 14.25 10C12.0409 10 10.25 11.7909 10.25 14C10.25 16.2091 12.0409 18 14.25 18Z"
            fill="#45AEF5"
          />
          <path
            opacity="0.32"
            d="M18.25 14C18.25 16.2091 16.4591 18 14.25 18C12.0409 18 10.25 16.2091 10.25 14C10.25 11.7909 12.0409 10 14.25 10C16.4591 10 18.25 11.7909 18.25 14Z"
            fill="#45AEF5"
          />
        </svg>
        <p class="text-[12px] font-bold text-[#45AEF5]">Settings</p>
      </div>
    </router-link>
  </div>
</template>

<script>
export default {
  data() {
    return {
      randomPh: [],
    };
  },
  created() {
    const keys = localStorage.getItem("publicArr");
    const res = keys.split(",");
    this.randomPh = res;
  },
};
</script>

<style lang="scss" scoped>
.c {
  display: grid;
  grid-template-rows: repeat(6, minmax(0px, 1fr));
  grid-auto-flow: column;
  gap: 2rem;
  place-content: space-evenly;
  margin: 1rem 0px;
  white-space: normal;
}
</style>
