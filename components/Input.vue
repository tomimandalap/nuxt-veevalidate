<script setup lang="ts">
import { useField } from "vee-validate";
const show = ref(false);

const props = defineProps({
  name: { type: String, required: true },
  maxLength: {
    type: Number,
    default: 100,
  },
  type: {
    type: String,
    default: "text",
    required: true,
  },
  placeholder: {
    type: String,
    default: "Placeholder",
  },
});

const isPassword = computed(() => ["password"].includes(props.type));

const { name } = toRefs(props);
const { value, errorMessage } = useField(name);
</script>

<template>
  <div class="relative">
    <input
      v-model="value"
      :name="name"
      :type="show ? 'text' : type"
      :placeholder="placeholder"
      :maxlength="maxLength"
      :class="
        !!errorMessage
          ? 'border-2 border-red-500'
          : 'border border-gray-300 mb-5 focus:ring-blue-500 focus:border-blue-500'
      "
      class="bg-white text-gray-900 text-sm rounded-full block w-full p-2.5"
    />
    <div
      v-show="isPassword"
      :class="errorMessage && '-mt-6'"
      class="absolute inset-y-0 right-2.5 flex items-center"
    >
      <button
        type="button"
        class="p-2.5 border-0 hover:cursor rounded-full"
        @click="show = !show"
      >
        <IconsEye v-if="show" />
        <IconsEyeSlash v-else />
      </button>
    </div>

    <p class="text-left mb-2">
      <small class="text-red-400 capitalize">{{ errorMessage }}</small>
    </p>
  </div>
</template>
