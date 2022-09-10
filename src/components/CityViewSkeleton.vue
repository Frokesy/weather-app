
<template>
    <div class="flex flex-col flex-1">
      <!-- Overview -->
      <div class="flex flex-col py-12 items-center d-1">
        <AnimatedPlaceHolder class="max-w-[300px] w-full mb-2 ph-1" />
        <AnimatedPlaceHolder class="max-w-[300px] w-full mb-12 ph-2" />
        <AnimatedPlaceHolder
          class="max-w-[300px] h-[100px] w-full mb-12 ph-3"
        />
        <AnimatedPlaceHolder class="max-w-[300px] w-full mb-8 ph-4" />
        <AnimatedPlaceHolder
          class="max-w-[300px] h-[75px] w-full ph-5"
        />
      </div>
      <!-- Hourly -->
      <div class="flex flex-col py-12 px-8 items-center d-1">
        <AnimatedPlaceHolder
          class="max-w-screen-md h-[100px] w-full mb-12 ph-3"
        />
      </div>
      <!-- Weekly -->
      <div class="flex flex-col py-12 px-8 items-center d-1">
        <AnimatedPlaceHolder
          class="max-w-screen-md h-[100px] w-full mb-12 ph-3"
        />
      </div>
    </div>
  </template>
  
  <script lang="ts">
import { defineComponent } from "vue";
import AnimatedPlaceHolder from "./AnimatedPlaceHolder.vue";

export default defineComponent({
    components: { AnimatedPlaceHolder },
});
  </script>
  <style>
   .d-1 {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-top: 3rem;
    padding-bottom: 3rem;
    padding-left: 2rem;
    padding-right: 2rem;
   }
   .ph-1 {
    max-width: 300px;
    width: 100%;
    margin-bottom: 0.5rem;
   }
   .ph-2 {
    max-width: 300px;
    width: 100%;
    margin-bottom: 3rem;
   }
   .ph-3 {
    max-width: 640px;
    height: 100px;
    width: 100%;
    margin-bottom: 3rem;
   }
    .ph-4 {
      max-width: 300px;
      width: 100%;
      margin-bottom: 2rem;
    }
    .ph-5 {
      max-width: 300px;
      height: 75px;
      width: 100%;
    }

  </style>