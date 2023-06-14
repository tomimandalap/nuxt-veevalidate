<script setup lang="ts">
import { object, string } from "yup";
import { useForm } from "vee-validate";

// Ex: TMP1234 or TP1234
const privyidRegex = /(^[a-zA-Z]{2,3})+(\d{4})?$/;
const onlyPassword = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[a-zA-Z\d]{8,12}$/;
const rulesSchema = object({
  privyid: string()
    .required("Field tidak boleh kosong")
    .min(4, "Minimal input 4 karakter")
    .matches(privyidRegex, "Privy ID tidak valid"),
  password: string()
    .required("Field tidak boleh koson")
    .min(8, "Minimal input 8 karakter")
    .max(12, "Maksimum input 12 karakter")
    .matches(onlyPassword, "Ex: passworD12, tidak boleh spesail karakter"),
});

const { handleSubmit } = useForm({
  validationSchema: rulesSchema,
});

const onSubmit = handleSubmit((value) => {
  console.log(value);
});
</script>

<template>
  <div class="bg-slate-50 min-h-screen flex justify-center items-center">
    <div class="border shadow-lg rounded-lg p-8 bg-white text-center w-[360px]">
      <img src="logo.svg" alt="logo privy" class="w-[80px] mx-auto mt-2" />
      <h3 class="text-lg font-medium mt-10">Hi, Welcome Back 👋</h3>
      <p class="text-xs text-gray-400 mb-10">It's good to see you again</p>

      <form @submit.prevent="onSubmit">
        <!-- PRIVYID -->
        <Input
          name="privyid"
          type="text"
          placeholder="ABXXXX0"
          :max-length="8"
        ></Input>

        <!-- PASSWORD -->
        <Input
          name="password"
          type="password"
          placeholder="Password"
          :max-length="16"
        ></Input>

        <NuxtLink to="/" class="text-gray-400 text-xs underline"
          >Forgot your PrivyID or Password?</NuxtLink
        >

        <button
          type="submit"
          class="bg-red-600 rounded-full w-full text-white p-2.5 mt-10 mb-10"
        >
          CONTINUE
        </button>
      </form>

      <small class="text-xs text-gray-300">Log In with</small>
      <button
        type="button"
        class="bg-white rounded-full w-full text-gray-400 flex justify-center items-center p-2.5"
      >
        <img src="qr.svg" alt="qr code" /> <span class="ml-3">QR Code</span>
      </button>
    </div>
  </div>
</template>
