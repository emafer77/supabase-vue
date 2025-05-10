<template>
  <div class="dashboard">
    <h1>Dashboard</h1>
  </div>
</template>

<script setup>
import { useAuth } from "../composables/useAuth";
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
