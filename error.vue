<script setup lang="ts">
const error = useError();

const handleError = () => {
  clearError({
    redirect: "/",
  });
};
</script>

<template>
  <div class="flex h-screen justify-center items-center flex-col">
    <h1 class="text-9xl">ERROR</h1>
    <p class="mt-7 text-4xl">{{ error?.message }}</p>

    <button
      class="rounded mt-7 text-lg bg-gray-700 px-7 py-2 text-white"
      @click="handleError"
    >
      Go Back
    </button>
  </div>
</template>
