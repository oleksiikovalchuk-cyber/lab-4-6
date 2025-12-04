<script setup lang="ts">
// Імпортуємо картинку для другої сторінки
import heroImage from '@/assets/second_photo.webp';
</script>

<template>
  <div class="w-full h-full flex flex-col items-center justify-evenly py-4">
    
    <section
      class="w-full h-[35%] max-h-[250px] bg-center bg-contain bg-no-repeat shrink-1"
      :style="{ backgroundImage: `url(${heroImage})` }"
      role="img"
      aria-label="Chat with ease illustration">
    </section>

    <div class="flex justify-center w-full shrink-0">
      <button
        type="button"
        class="flex justify-center items-center gap-[10px] w-[208px] h-[50px] bg-[#FF5F5F] text-white rounded-[5px] tracking-[0.05em] font-bold text-[20px] leading-[24px] outline-none border-0 font-['Lato'] shadow-none hover:opacity-90 transition-opacity cursor-default">
        CHAT WITH EASE
      </button>
    </div>

    <section class="flex justify-center px-[40px] shrink-0">
      <p class="w-full max-w-[275px] m-0 text-center text-[#5A5A64] font-normal text-[10px] leading-[14px] font-['Lato']">
        Maecenas in placerat nibh. Integer sollicitudin sapien et massa varius venenatis.
        Nulla facilisis purus nec nibh posuere volutpat. Nunc congue, arcu sit amet imperdiet
        sodales, tellus odio sagittis turpis, sed tincidunt nibh urna in leo. Duis et sodales
        elit, ut cursus est. Aenean magna metus, volutpat vel dignissim quis, malesuada eget ex.
      </p>
    </section>

  </div>
</template>