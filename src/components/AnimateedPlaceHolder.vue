<template>
    <div class="animate-pulse bg-gradient-to-r from-gray-100 animate">
      &nbsp;
    </div>
</template>
<style>
    .animate {
        animation: pulse 1s cubic-bezier(0.4, 0, 0.6, 1) infinite;
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