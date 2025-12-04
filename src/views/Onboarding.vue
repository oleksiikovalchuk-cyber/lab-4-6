<script setup lang="ts">
import { ref, computed } from 'vue';
import { useRouter } from 'vue-router';

import OnboardPage1 from '../components/OnboardPage1.vue';
import OnboardPage2 from '../components/OnboardPage2.vue';
import OnboardPage3 from '../components/OnboardPage3.vue';

const router = useRouter();
const currentStep = ref(0);
const steps = [OnboardPage1, OnboardPage2, OnboardPage3];
const currentComponent = computed(() => steps[currentStep.value]);

const nextStep = () => {
  if (currentStep.value < steps.length - 1) {
    currentStep.value++;
  } else {
    finishOnboarding();
  }
};

const goToStep = (index: number) => {
  currentStep.value = index;
};

const finishOnboarding = () => {
  router.push('/login');
};
</script>

<template>
  <div class="h-[100dvh] w-full bg-[#eaeaea] font-['Lato'] overflow-hidden block md:flex md:items-center md:justify-center md:p-4 supports-[height:100dvh]:h-[100dvh]">

    <main class="relative w-full h-full bg-white flex flex-col overflow-hidden transition-all duration-300
                 md:max-w-[375px] md:h-[90vh] md:max-h-[812px] md:rounded-[24px] md:shadow-2xl shadow-none rounded-none">
      
      <div class="flex-grow flex flex-col overflow-hidden min-h-0">
        <Transition name="fade" mode="out-in">
          <component :is="currentComponent" :key="currentStep" class="h-full w-full" />
        </Transition>
      </div>

      <footer class="h-[70px] shrink-0 flex items-center justify-between px-6 pb-4 bg-white z-10">
        <button
          @click="finishOnboarding"
          type="button"
          class="w-[70px] h-[30px] rounded-[5px] text-[12px] leading-[14px] tracking-[0.1em] font-semibold bg-[#F5F5FF] text-[#32323C] border-0 outline-none hover:bg-gray-200 transition-colors cursor-pointer">
          SKIP
        </button>

        <div class="flex items-center gap-5" aria-label="pagination">
          <button 
            v-for="(step, index) in steps" 
            :key="index"
            @click="goToStep(index)"
            type="button"
            class="block w-[10px] h-[10px] rounded-[1px] border-none p-0 cursor-pointer transition-colors duration-300"
            :class="index === currentStep ? 'bg-[#FF5F5F]' : 'bg-[#F5F5FF]'"
            :aria-label="'Go to step ' + (index + 1)"
          ></button>
        </div>

        <button
          @click="nextStep"
          type="button"
          class="w-[70px] h-[30px] rounded-[5px] text-[12px] leading-[14px] tracking-[0.1em] font-semibold bg-[#FF5F5F] text-white border-0 outline-none hover:bg-red-500 transition-colors cursor-pointer">
          NEXT
        </button>
      </footer>

    </main>
  </div>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>