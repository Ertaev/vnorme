<script setup>
import { ref } from "vue";
import { RouterView } from "vue-router";

import Header from "@/components/Header.vue"
import MobileMenu from "@/components/MobileMenu.vue"
import Footer from "@/components/Footer.vue"

const mobileMenuActive = ref(false)

const toggleMobileMenu = () => {
    mobileMenuActive.value = !mobileMenuActive.value

    document.documentElement.style.overflow = mobileMenuActive.value ? "hidden" : "auto"
}

</script>

<template>
    <Header @toggleMobileMenu="toggleMobileMenu" />

    <MobileMenu :mobileMenuActive="mobileMenuActive" @toggleMobileMenu="toggleMobileMenu" />

    <main>
        <RouterView />
    </main>

    <Footer />
</template>

<style scoped>

</style>
