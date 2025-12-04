<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';
// Переконайся, що у тебе є картинка за цим шляхом
import logoImg from '@/assets/Vector.png';

const router = useRouter();

// Поля форми
const username = ref('');
const password = ref('');
const email = ref('');

// Об'єкт для помилок
const errors = ref({
  username: '',
  email: '',
  password: ''
});

// Функція перевірки email
const isValidEmail = (email: string) => {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
};

// Валідація (Українською)
const validateForm = () => {
  let isValid = true;
  errors.value = { username: '', email: '', password: '' };

  // 1. Ім'я
  if (!username.value.trim()) {
    errors.value.username = "Введіть ім'я користувача";
    isValid = false;
  } else if (username.value.length < 3) {
    errors.value.username = "Мінімум 3 символи";
    isValid = false;
  }

  // 2. Email
  if (!email.value.trim()) {
    errors.value.email = "Введіть Email";
    isValid = false;
  } else if (!isValidEmail(email.value)) {
    errors.value.email = "Некоректний формат Email";
    isValid = false;
  }

  // 3. Пароль
  if (!password.value) {
    errors.value.password = "Введіть пароль";
    isValid = false;
  } else if (password.value.length < 8) {
    errors.value.password = "Мінімум 8 символів";
    isValid = false;
  }

  return isValid;
};

const handleRegister = () => {
  if (validateForm()) {
    console.group('✅ Registration Success');
    console.log('Username:', username.value);
    console.log('Email:', email.value);
    console.log('Password:', password.value);
    console.groupEnd();
    
    // Тут можна додати логіку відправки на бекенд
    // router.push('/login');
  } else {
    console.log('❌ Validation Failed');
  }
};

const goToLogin = () => {
  router.push('/login');
};
</script>

<template>
  <!-- 
    ГОЛОВНИЙ КОНТЕЙНЕР (Адаптивний):
    - h-[100dvh]: фіксує висоту на весь екран мобільного.
    - md:flex: центрує картку на комп'ютері.
  -->
  <div class="h-[100dvh] w-full bg-[#eaeaea] font-['Lato'] overflow-hidden block md:flex md:items-center md:justify-center md:p-4 supports-[height:100dvh]:h-[100dvh]">

    <main
      class="relative w-full h-full bg-[#FF5F5F] overflow-hidden flex flex-col items-center py-8 transition-all duration-300
             md:max-w-[375px] md:h-[90vh] md:max-h-[812px] md:rounded-[24px] md:shadow-2xl
             shadow-none rounded-none"
    >
      <div class="w-full h-full flex flex-col items-center justify-evenly overflow-y-auto px-6 scrollbar-hide">

        <!-- Логотип -->
        <div class="flex flex-col items-center shrink-0">
          <img :src="logoImg" class="mb-4 max-w-[80px] h-auto" alt="Logo" />
          <h1 class="font-['Fredoka_One'] text-[35px] text-white tracking-[0.05em]">
            FATED
          </h1>
        </div>

        <!-- Таби (Кнопки зверху) -->
        <div class="flex gap-[20px] shrink-0">
          <!-- Кнопка Login (Веде назад, прозора) -->
          <button
            @click="goToLogin"
            class="w-[130px] h-[30px] rounded-[5px] text-[12px] font-extrabold tracking-[0.1em] uppercase transition-all bg-white/20 text-white hover:bg-white/30"
          >
            Login
          </button>

          <!-- Кнопка Register (Активна, біла) -->
          <button
            class="w-[130px] h-[30px] rounded-[5px] text-[12px] font-extrabold tracking-[0.1em] uppercase transition-all bg-white text-[#FF5F5F] cursor-default"
          >
            Register
          </button>
        </div>

        <!-- ФОРМА РЕЄСТРАЦІЇ -->
        <form
          @submit.prevent="handleRegister"
          class="flex flex-col items-center w-full gap-3 shrink-0"
        >
          <!-- Username Input -->
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

          <!-- Password Input -->
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

          <!-- Email Input -->
          <div class="w-full max-w-[280px] flex flex-col">
            <input
              v-model="email"
              type="email"
              placeholder="email"
              class="w-full h-[50px] bg-white rounded-[5px] text-center text-[15px] tracking-[0.1em] text-[#32323C] placeholder:text-[#32323C]/70 outline-none border-2 transition-colors"
              :class="errors.email ? 'border-red-800' : 'border-transparent focus:border-white/50'"
            />
            <span v-if="errors.email" class="text-white text-[10px] font-bold mt-1 text-center bg-red-700/20 py-0.5 rounded shadow-sm">
              {{ errors.email }}
            </span>
          </div>

          <a href="#" class="w-full max-w-[280px] text-right text-white text-[10px] tracking-[0.1em] py-2 no-underline hover:underline">
            FORGOT PASSWORD?
          </a>

          <button
            type="submit"
            class="w-full max-w-[280px] h-[50px] bg-white rounded-[5px] shadow-md font-extrabold text-[15px] text-[#FF5F5F] uppercase tracking-[0.1em] active:scale-95 transition-transform hover:bg-gray-50"
          >
            REGISTER
          </button>
        </form>

        <!-- Нижній текст -->
        <div class="shrink-0 text-center">
          <p class="text-white text-[10px] tracking-[0.1em] uppercase">
            Already have an account? 
            <!-- ТУТ ВИКОРИСТАНО font-extrabold ДЛЯ ЖИРНОГО ШРИФТУ -->
            <a href="#"
               @click.prevent="goToLogin"
               class="font-extrabold text-white no-underline hover:underline ml-1"
            >
              LOGIN
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