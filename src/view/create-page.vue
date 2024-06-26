<template>
  <div class="relative" v-if="!open && !inputBool">
    <router-link to="/">
      <p
        class="bg-[#1D2633] absolute px-[15px] py-[7px] rounded-[20px] font-[600] right-0 text-[13px]"
      >
        Sign Out
      </p>
    </router-link>
    <div class="b">
      <div class="text-center">
        <img src="../assets/image.png" alt="" class="centered-image" />
        <p class="font-bold text-[24px]">Grab a pen and a piece of paper</p>
        <p class="gr text-[14px]">
          We strongly recommend you write down the recovery phrase because it’s
          the only way to have access to and recover your wallet in case of
          losing your device. Do not send it to yourself via email or take a
          screenshot. It’s safer when kept offline.
        </p>
        <div
          class="mt-[20px] bg-[#45AEF5] py-[18px] rounded-[17px] cursor-pointer"
          @click="randomsPh()"
        >
          <p class="text-center font-[600]">Continue</p>
        </div>
      </div>
    </div>
  </div>
  <div v-if="open && !inputBool">
    <div class="b2">
      <div class="">
        <p class="font-bold text-[24px] text-center">Your recovery phrase</p>
        <p class="gr text-center">
          Write down these 24 words in the order given below and store them in a
          secret, safe place.
        </p>
        <div class="c">
          <span
            v-for="(phrase, index) in randomPh"
            class="text-[16px] ml-[15px]"
          >
            <span class="gr mr-[10px]">{{ index + 1 }}</span> {{ phrase }}
          </span>
        </div>
        <div
          class="mt-[20px] bg-[#45AEF5] py-[18px] rounded-[17px] cursor-pointer"
          @click="inputBool = !inputBool"
        >
          <p class="text-center font-[600]">Continue</p>
        </div>
      </div>
    </div>
  </div>
  <div>
    <div class="validate" v-if="inputBool && !passBool">
      <div class="b">
        <div class="text-center">
          <p class="font-bold text-[24px]">So, let’s check</p>
          <p class="gr text-[16px]" @click="a">
            To check whether you’ve written down your recovery phrase correctly,
            please enter the
            <span v-for="i in selectedWords">{{ i.index + 1 }}, </span> words
          </p>
          <div
            :class="{ 'invalid-div': !isValid[index] }"
            class="bg-[#1D2633] p-[15px] rounded-[15px] flex mt-[20px]"
            v-for="(item, index) in selectedWords"
            :key="index"
          >
            <span class="gr">{{ item.index + 1 }}</span>
            <input
              autocomplete="off"
              type="text"
              class="bg-[#1D2633] ml-[20px] w-[100%]"
              :class="{ 'invalid-input': !isValid[index] }"
              v-model="inputWord[index]"
              @input="validateWord(index)"
            />
          </div>
          <div
            @click="validateInputs"
            :class="{ disabled: !isAllValid }"
            class="mt-[20px] bg-[#45AEF5] py-[18px] rounded-[17px] cursor-pointer"
          >
            <p class="text-center font-[600]">Continue</p>
          </div>
        </div>
      </div>
    </div>

    <div v-if="passBool">
      <div class="b">
        <div class="text-center w-[100%]">
          <p class="font-bold text-[24px]">Create password</p>

          <div class="pt-[20px]">
            <input
              type="password"
              id="password"
              v-model="password"
              class="bg-[#1D2633] text-[white] text-sm rounded-[15px] focus:ring-blue-500 focus:border-blue-500 block w-full dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 p-[15px] h-[60px] text-[20px]"
              placeholder="Password"
              required
            />
          </div>
          <p class="text-left gr pt-[10px] text-[14px]">
            Must be at least 6 characters.
          </p>
          <div class="pt-[20px]">
            <input
              type="password"
              id="confirmPassword"
              v-model="confirmPassword"
              class="bg-[#1D2633] text-[white] text-sm rounded-[15px] focus:ring-blue-500 focus:border-blue-500 block w-full dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 p-[15px] h-[60px] text-[20px]"
              placeholder="Re-enter password"
              required
            />
          </div>

          <div
            @click="validatePasswords"
            :class="{ disabled: !arePasswordsValid }"
            class="mt-[20px] bg-[#45AEF5] py-[18px] rounded-[17px] cursor-pointer"
          >
            <p class="text-center font-[600]">Continue</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { getHttpEndpoint } from "@orbs-network/ton-access";
import {
  mnemonicToWalletKey,
  mnemonicNew,
  mnemonicToPrivateKey,
  mnemonicValidate,
} from "@ton/crypto";
import { WalletContractV4, TonClient, fromNano } from "@ton/ton";

export default {
  data() {
    return {
      open: false,
      phrases: [
        "select",
        "chuckle",
        "upgrade",
        "flee",
        "process",
        "zebra",
        "subway",
        "cross",
        "diamond",
        "laundry",
        "version",
        "own",
        "jungle",
        "wolf",
        "praise",
        "rule",
        "post",
        "pigeon",
        "board",
        "differ",
        "morning",
        "memory",
        "solar",
        "demise",
      ],
      phras:
        "select chuckle upgrade flee process zebra subway cross diamond laundry version own jungle wolf praise rule post pigeon board differ morning memory solar demise",
      inputBool: false,
      passBool: false,
      selectedWords: [],
      randomPh: [],
      itemInput: "",
      inputWord: [],
      isValid: [],
      password: "",
      confirmPassword: "",
    };
  },
  computed: {
    isAllValid() {
      return this.inputWord.every((word) => word.trim() !== "");
    },
    arePasswordsValid() {
      return (
        this.password.length >= 6 && this.password === this.confirmPassword
      );
    },
  },

  methods: {
    validatePasswords() {
      if (!this.arePasswordsValid) {
        return;
      }
      this.addWallet();
    },
    async addWallet() {
      const key = await mnemonicToPrivateKey(this.randomPh);
      const wallet = WalletContractV4.create({
        publicKey: key.publicKey,
        workchain: 0,
      });
      localStorage.setItem("publicArr", this.randomPh);
      const endpoint = await getHttpEndpoint({ network: "testnet" });
      const client = new TonClient({ endpoint });
      const balance = await client.getBalance(wallet.address);
      this.balance = fromNano(balance);
      console.log(wallet.address.toString({ testOnly: true }));
      this.$router.push("/wallet");
    },
    async randomsPh() {
      this.randomPh = await mnemonicNew(12);
      this.open = !this.open;
      this.getRandomWords();
      console.log(this.randomPh);
    },
    validateInputs() {
      if (this.inputWord.every((word) => !word.trim())) {
        return;
      }
      this.passBool = !this.passBool;
    },
    async validateWord(index) {
      if (!this.inputWord[index]) {
        this.isValid[index] = true;
        return;
      }
      const isBool = await mnemonicValidate(this.randomPh);
      if (isBool) {
        this.isValid[index] = this.randomPh.includes(this.inputWord[index]);
        console.log(this.isValid);
      }
    },
    getRandomWords() {
      const tempArray = [...this.randomPh];
      this.selectedWords = [];
      this.isValid = [];

      for (let i = 0; i < 3; i++) {
        const randomIndex = Math.floor(Math.random() * tempArray.length);
        const wordObject = {
          index: this.randomPh.indexOf(tempArray[randomIndex]),
          text: tempArray[randomIndex],
        };
        this.selectedWords.push(wordObject);
        tempArray.splice(randomIndex, 1);
      }
    },
  },
  async created() {},
};
</script>

<style lang="scss" scoped>
.disabled {
  pointer-events: none; /* Делаем кнопку некликабельной */
  opacity: 0.5; /* Уменьшаем прозрачность кнопки */
}
.b {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.b2 {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.centered-image {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.c {
  display: grid;
  grid-template-rows: repeat(6, minmax(0px, 1fr));
  grid-auto-flow: column;
  gap: 0.5rem;
  place-content: space-evenly;
  margin: 1rem 0px;
  white-space: normal;
}
.invalid-input {
  background-color: rgba(255, 71, 102, 0.001);
}
.invalid-div {
  background-color: rgba(255, 71, 102, 0.08);
}
</style>
