<template>
  <div>
    <div class="grid-cols-3">
      <div></div>
      <div></div>

      <div>
        <nav class="p-4 bg-linear-to-r from-black via-stone-500 to-stone-600">
          <div class="flex justify-between items-center">
            <h1 class="text-2xl font-bold text-white">Mi Tienda</h1>
            <p v-if="user" class="text-white">Bienvenido, {{ user.email }}</p>

            <div class="flex gap-6 text-white text-lg">
              <router-link
                to="/"
                class="hover:underline transition duration-200"
              >
                Home
              </router-link>

              <router-link
                v-if="user"
                to="/dashboard"
                class="hover:underline transition duration-200"
              >
                Dashboard
              </router-link>
            </div>
            <div>
              <button
                v-if="user"
                @click="handleSignOut"
                class="text-white hover:underline"
              >
                cerrar sesion
              </button>
              <router-link
                v-if="!user"
                to="/login"
                class="hover:underline transition duration-200 text-amber-50"
              >
                Iniciar Sesión
              </router-link>
            </div>
          </div>
        </nav>
      </div>
    </div>
    <router-view />
  </div>
</template>

<script setup>
import { useAuth } from "./composables/useAuth";
import { useRouter } from "vue-router";

const router = useRouter();
const { user, signOut } = useAuth();
const handleSignOut = async () => {
  try {
    await signOut();
    router.push("/login");
  } catch (error) {
    console.error("Error:", error.message);
  }
};
</script>
