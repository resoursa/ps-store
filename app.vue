<template>
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>

<script setup>
import { useRoute, useRouter } from "vue-router";

const router = useRouter();
const route = useRoute();

// Redirect to /store if the current route is the root
if (route.path === "/") {
  router.push("/store");
}
</script>
