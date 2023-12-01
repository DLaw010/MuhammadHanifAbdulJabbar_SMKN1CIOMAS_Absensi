<script lang="ts" setup>
import { useAuthStore } from "~/stores/auth"
const authStore = useAuthStore();
const isAuthenticated = ref();
const router = useRouter();

isAuthenticated.value = useCookie("access_token").value;

const logout = async () => {
await authStore.logout();
const accessToken = useCookie("access_token");
const refreshToken = useCookie("refresh_token");
accessToken.value = null;
refreshToken.value = null;
setTimeout(() => {
isAuthenticated.value = useCookie("access_token").value;
}, 100);
router.push({
path: "/"
})
}
</script>

<template>
    <header class="w-full border-b border-slate-200 py-6">
    <div class="container">
    <div class="flex justify-between items-center">
    <div>
    <NuxtLink to="/" class="text-xl font-bold">Absen Cuy</NuxtLink>
    </div>
    <nav class="flex items-center gap-6">
    <NuxtLink to="/" class="text-base">Beranda</NuxtLink>
    
    <NuxtLink to="/product" class="text-
    base">Absen</NuxtLink>
    
    
    <NuxtLink v-if="!isAuthenticated" to="/login" class="text-base bg-amber-400 px-6 py-2 text-white rounded-lg hover:bg-amber-600/80">Login</NuxtLink>
<div v-else class="text-base cursor-pointer bg-red-600 px-6 py-2 text-white rounded-lg hover:bg-gray-600/80" @click="logout">Logout</div>
    </nav>
    </div>
    </div>
    </header>
    </template>