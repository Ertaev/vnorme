<template>
    <header class="header">
        <div class="container">
            <div class="header__inner">
                <Logo />

                <ul class="nav">
                    <li
                        v-for="navItem of navList"
                        class="nav__item"
                        :key="navItem.id"
                    >
                        <RouterLink
                            :to="navItem.link"
                            :class="{ active: navItem.isActive }"
                        >
                            {{ navItem.title }}
                        </RouterLink>
                    </li>
                </ul>

                <RouterLink to="/" class="button button--white"> Войти </RouterLink>

                <div class="burger" @click="() => emit('toggleMobileMenu')">
                    <span></span>
                    <span></span>
                    <span></span>
                </div>
            </div>
        </div>
    </header>
</template>

<script setup>
import { ref } from "vue";

import Logo from "@/components/Logo.vue"

const emit = defineEmits(["toggleMobileMenu"]);

const navList = ref([
    {
        id: 1,
        title: "Стать психологом Vnorme",
        isActive: false,
        link: "/",
    },
    {
        id: 2,
        title: "Для психологов",
        isActive: false,
        link: "/",
    },
    {
        id: 3,
        title: "Подобрать психолога",
        isActive: true,
        link: "/",
    },
    {
        id: 4,
        title: "Контакты",
        isActive: false,
        link: "/",
    },
]);


</script>

<style scoped>
.header__inner {
    padding: 20px 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.nav {
    display: flex;
    align-items: center;
    gap: 24px;
}

.nav__item a {
    font-weight: 700;
    font-size: 16px;
    line-height: 24px;

    color: #030303;
}

.nav__item a:hover {
    color: #818181;
}

.nav__item a:active,
.nav__item a.active {
    color: #0c9733;
}

.header .button {
    width: 89px;
}

.burger {
    display: none;
    flex-direction: column;

    gap: 9px;

    cursor: pointer;
}

.burger span {
    width: 36px;
    height: 2px;
    border-radius: 10px;

    background: #000;
}

@media screen and (max-width: 1200px) {
    .nav {
        gap: 16px;
    }
}

@media screen and (max-width: 992px) {
    .nav,
    .header .button {
        display: none;
    }

    .burger {
        display: flex;
    }
}
</style>
