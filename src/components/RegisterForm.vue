<template>
  <div
    class="flex justify-center items-center min-h-screen bg-gradient-to-br from-gray-800 via-blue-700 to-gray-900"
  >
    <div class="w-full max-w-md bg-white shadow-xl rounded-2xl p-8">
      <h2 class="text-3xl font-bold text-violet-800 mb-6 text-center">
        Registrarse
      </h2>
      <form @submit.prevent="handleRegister" class="space-y-4">
        <div>
          <label for="email" class="block text-sm font-medium text-gray-700"
            >Email:</label
          >
          <input
            type="email"
            id="email"
            v-model="email"
            required
            placeholder="tucorreo@ejemplo.com"
            class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-violet-500 focus:outline-none"
          />
        </div>

        <div>
          <label for="password" class="block text-sm font-medium text-gray-700"
            >Contraseña:</label
          >
          <input
            type="password"
            id="password"
            v-model="password"
            required
            placeholder="Tu contraseña"
            class="w-full px-4 py-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-violet-500 focus:outline-none"
          />
        </div>

        <button
          type="submit"
          :disabled="loading"
          class="w-full py-2 px-4 bg-violet-700 text-white font-semibold rounded-md hover:bg-violet-800 disabled:opacity-50 transition"
        >
          {{ loading ? "Cargando..." : "Registrarse" }}
        </button>

        <p v-if="error" class="text-red-600 text-sm text-center mt-2">
          {{ error }}
        </p>
        <p v-if="success" class="success">{{ success }}</p>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { supabase } from "../lib/supabase";

const email = ref("");
const password = ref("");
const loading = ref(false);
const error = ref("");
const success = ref("");

const handleRegister = async () => {
  try {
    loading.value = true;
    error.value = "";
    success.value = "";

    const { data, error: signUpError } = await supabase.auth.signUp({
      email: email.value,
      password: password.value,
    });

    if (signUpError) throw signUpError;

    success.value = "Registro exitoso! Revisa tu email.";
  } catch (err) {
    error.value = err.message;
  } finally {
    loading.value = false;
  }
};
</script>
