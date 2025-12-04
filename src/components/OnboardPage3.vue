<script setup lang="ts">
import heroImage from '@/assets/thrid_photo.png';
</script>

<template>
  <div class="w-full h-full flex flex-col items-center justify-evenly py-4">
    
    <section
      class="w-full h-[35%] max-h-[250px] bg-center bg-contain bg-no-repeat shrink-1"
      :style="{ backgroundImage: `url(${heroImage})` }"
      role="img"
      aria-label="Find your match illustration">
    </section>

    <div class="flex justify-center w-full shrink-0">
      <button
        type="button"
        class="flex justify-center items-center gap-[10px] w-[229px] h-[50px] bg-[#FF5F5F] text-white rounded-[5px] tracking-[0.05em] font-bold text-[20px] leading-[24px] outline-none border-0 font-['Lato'] shadow-none hover:opacity-90 transition-opacity cursor-default">
        FIND YOUR MATCH
      </button>
    </div>

    <section class="flex justify-center px-[40px] shrink-0">
      <p class="w-full max-w-[275px] m-0 text-center text-[#5A5A64] font-normal text-[10px] leading-[14px] font-['Lato']">
        Nam vitae convallis nulla. Aenean a orci in ipsum congue convallis ac tempus nibh.
        Donec porttitor ut diam dignissim. Aliquam erat volutpat. Cras maximus tempus elit
        bibendum sodales. Ut id augue rhoncus, egestas lorem nec, varius lacus.
      </p>
    </section>

  </div>
</template>