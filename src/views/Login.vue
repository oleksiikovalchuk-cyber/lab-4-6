<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import logoImg from '@/assets/Vector.png';

const router = useRouter();

const username = ref('');
const password = ref('');


const errors = ref({
  username: '',
  password: ''
});


const validateForm = () => {
  let isValid = true;
  errors.value = { username: '', password: '' };


  if (!username.value.trim()) {
    errors.value.username = "Введіть ім'я користувача";
    isValid = false;
  } else if (username.value.length < 3) {
    errors.value.username = "Ім'я має містити мінімум 3 символи";
    isValid = false;
  }


  if (!password.value) {
    errors.value.password = "Введіть пароль";
    isValid = false;
  } else if (password.value.length < 8) {
    errors.value.password = "Пароль має містити мінімум 8 символів";
    isValid = false;
  }

  return isValid;
};

const handleLogin = () => {
  if (validateForm()) {
    console.group('✅ Login Success');
    console.log('Username:', username.value);
    console.log('Password:', password.value);
    console.groupEnd();
    

  } else {
    console.log('❌ Validation Failed');
  }
};


const goToRegister = () => {
  router.push('/register'); 
};
</script>

<template>
  <div class="h-[100dvh] w-full bg-[#eaeaea] font-['Lato'] overflow-hidden block md:flex md:items-center md:justify-center md:p-4 supports-[height:100dvh]:h-[100dvh]">

    <main
      class="relative w-full h-full bg-[#FF5F5F] overflow-hidden flex flex-col items-center py-8 transition-all duration-300
             md:max-w-[375px] md:h-[90vh] md:max-h-[812px] md:rounded-[24px] md:shadow-[0_0_20px_rgba(0,0,0,0.15)]
             shadow-none rounded-none"
    >
      <div class="w-full h-full flex flex-col items-center justify-evenly overflow-y-auto px-6 scrollbar-hide">


        <div class="flex flex-col items-center shrink-0">
          <img :src="logoImg" class="mb-4 max-w-[80px] h-auto" alt="Logo" />
          <h1 class="font-['Fredoka_One'] text-[35px] text-white tracking-[0.05em]">
            FATED
          </h1>
        </div>


        <div class="flex gap-[20px] shrink-0">

          <button
            class="w-[130px] h-[30px] rounded-[5px] text-[12px] font-extrabold tracking-[0.1em] uppercase transition-all bg-white text-[#FF5F5F] cursor-default"
          >
            Login
          </button>

          <button
            @click="goToRegister"
            class="w-[130px] h-[30px] rounded-[5px] text-[12px] font-extrabold tracking-[0.1em] uppercase transition-all bg-white/20 text-white hover:bg-white/30"
          >
            Register
          </button>
        </div>

        <form
          @submit.prevent="handleLogin"
          class="flex flex-col items-center w-full gap-3 shrink-0"
        >
          <div class="w-full max-w-[280px] flex flex-col">
            <input
              v-model="username"
              type="text"
              placeholder="user name"
              class="w-full h-[50px] bg-white rounded-[5px] text-center text-[15px] tracking-[0.1em] text-[#32323C] placeholder:text-[#32323C]/70 outline-none border-2 transition-colors"
              :class="errors.username ? 'border-red-800' : 'border-transparent focus:border-white/50'"
            />
    
            <span v-if="errors.username" class="text-white text-[10px] font-bold mt-1 text-center bg-red-700/20 py-0.5 rounded shadow-sm">
              {{ errors.username }}
            </span>
          </div>

          <div class="w-full max-w-[280px] flex flex-col">
            <input
              v-model="password"
              type="password"
              placeholder="password"
              class="w-full h-[50px] bg-white rounded-[5px] text-center text-[15px] tracking-[0.1em] text-[#32323C] placeholder:text-[#32323C]/70 outline-none border-2 transition-colors"
              :class="errors.password ? 'border-red-800' : 'border-transparent focus:border-white/50'"
            />

            <span v-if="errors.password" class="text-white text-[10px] font-bold mt-1 text-center bg-red-700/20 py-0.5 rounded shadow-sm">
              {{ errors.password }}
            </span>
          </div>

          <a href="#" class="w-full max-w-[280px] text-right text-white text-[10px] tracking-[0.1em] py-2 no-underline hover:underline">
            FORGOT PASSWORD?
          </a>

          <button
            type="submit"
            class="w-full max-w-[280px] h-[50px] bg-white rounded-[5px] shadow-md font-extrabold text-[15px] text-[#FF5F5F] uppercase tracking-[0.1em] active:scale-95 transition-transform hover:bg-gray-50"
          >
            LOGIN
          </button>
        </form>


        <div class="shrink-0 text-center">
          <p class="text-white text-[10px] tracking-[0.1em] uppercase">
            Don't have an account? 
            <a href="#"
               @click.prevent="goToRegister"
               class="font-extrabold text-white no-underline hover:underline ml-1"
            >
              REGISTER
            </a>
          </p>
        </div>

      </div>
    </main>
  </div>
</template>

<style scoped>
.scrollbar-hide::-webkit-scrollbar {
  display: none;
}
.scrollbar-hide {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
</style>