
<template>
    <div class="animate-pulse bg-gradient-to-r from-gray-100 animate">
      &nbsp;
    </div>
</template>
<style>
    .animate {
        animation: pulse 1s cubic-bezier(0.4, 0, 0.6, 1) infinite;
        background: linear-gradient(
          to right,
          #f3f4f6 4%,
          #e5e7eb 25%,
          #f3f4f6 36%
        );
    }
    @keyframes pulse {
        0% {
            opacity: 1;
        }
        50% {
            opacity: 0.4;
        }
        100% {
            opacity: 1;
        }
    }
</style>
<script lang="ts">
import { defineComponent } from 'vue';

 export default defineComponent({
    name: "AnimatedPlaceHolder",
});
</script>