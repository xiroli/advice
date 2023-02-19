<script setup lang="ts">
  import dice from "../images/icon-dice.svg";
  import patternSm from "../images/pattern-divider-mobile.svg";
  import patternLg from "../images/pattern-divider-desktop.svg";
  import axios from "axios";
  import { onMounted, ref } from "vue";
type Advice = {
    slip: {
        id: number;
        advice: string;
    };
};
let advice = $ref("");
let adviceId = $ref(0);

   async function getAdvice() {
    const response = await axios.get<Advice>("https://api.adviceslip.com/advice");
    return response.data
   }
onMounted(async () => {
    const quote: Advice = await getAdvice();
    adviceId = quote.slip.id;
    advice = quote.slip.advice;
});

function newAdvice() {
    getAdvice().then((quote) => {
        adviceId= quote.slip.id;
        advice = quote.slip.advice;
    });
}
</script>

<template>
    <section class="card-container relative w-[350px] lg:w-[580px] h-[380px] pt-[50px] ">
        <div class="flex flex-col h-full items-center ">
            <h1 class="text-[28px] font-bold text-white">ADVICE #{{adviceId}}</h1>
            <div class="paragraph-container px-4 lg:px-16 pt-4 pb-12 mt-4">
                <p class="paragraph text-2xl lg:text-3xl">"{{advice}}"</p>
            </div>
        </div>
        <img :src="patternSm" class="absolute  right-1/2 translate-x-1/2 bottom-20 lg:hidden" alt="pattern" />
        <img :src="patternLg" class="absolute  right-1/2 translate-x-1/2 bottom-20 hidden lg:block" alt="pattern" />
      <div class="btn-container w-[65px] h-[65px] absolute right-1/2 -bottom-8 translate-x-1/2">
      <button class="btn w-full flex justify-center items-center h-full rounded-full " @click="newAdvice">
        <img :src="dice" class="" alt="dice" />
        </button>
    </div>
    </section>
</template>

<style scoped>
    .card-container {
        background: hsl(217, 19%, 24%);
        border-radius: 20px;
    }
    .btn {
        background: hsl(150, 100%, 66%);
    }
    .btn-container {
        cursor: pointer;
    }
    .btn-container .btn:hover {
        box-shadow: 0 0 40px hsl(150, 100%, 66%);
    }
    h1 {
        font-size: 15px;
        font-family: Manrope;
        color: hsl(150, 100%, 66%);
        letter-spacing: 5.5px;
    }
    .paragraph {
        font-family: Manrope;
        color: hsl(193, 38%, 86%);
    }
</style>
