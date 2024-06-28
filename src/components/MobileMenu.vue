<template>
	<div class="mobile-menu" :class="{opened: mobileMenuActive}">
        <div class="container">
            <div class="menu-top">
                <Logo />

                <div class="close" @click="() => emit('toggleMobileMenu')"></div>
            </div>

            <ul class="menu-nav">
                <li class="menu-nav__item">
                    <RouterLink to="/">Для психологов</RouterLink>
                </li>
                <li class="menu-nav__item">
                    <RouterLink to="/">Стать психологом Vnorme</RouterLink>
                </li>
                <li class="menu-nav__item">
                    <RouterLink to="/">Подобрать психолога</RouterLink>
                </li>
                <li class="menu-nav__item">
                    <RouterLink to="/">Контакты</RouterLink>
                </li>
            </ul>

            <RouterLink to="/" class="button button--gradient"> Войти </RouterLink>
        </div>
    </div>
</template>

<script setup>
import Logo from "@/components/Logo.vue";

defineProps({
	mobileMenuActive: Boolean
})

const emit = defineEmits(["toggleMobileMenu"])
</script>

<style scope>
.menu-top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 40px;
}

.mobile-menu {
    position: fixed;
    left: 0;
    top: -100vh;

    padding: 20px 0;

    width: 100%;
    height: 100vh;

    background: #fff;
    z-index: 100;

    transition: all .3s ease;
}

.mobile-menu.opened {
    top: 0;
}

.close {
    position: relative;

    width: 16px;
    height: 16px;

    display: flex;
    align-items: center;
    justify-content: center;

    cursor: pointer;
}

.close::before,
.close::after {
    content: "";
    position: absolute;

    width: 23px;
    height: 2px;

    background: #030303;

    border-radius: 10px;
}

.close::before {
    transform: rotate(45deg);
}

.close::after {
    transform: rotate(-45deg);
}

.menu-nav {
    display: flex;
    flex-direction: column;
    gap: 12px;
    margin-bottom: 40px;
}

.menu-nav__item a {
    display: flex;
    width: 100%;

    font-family: 'Inter';
    font-weight: 600;
    font-size: 14px;
    line-height: 21px;

    color: #818181;
    border-radius: 12px;

    padding: 9.5px 12px;

    transition: all .3s ease;
}

.menu-nav__item a:hover,
.menu-nav__item a:active {
    color: #1D1B20;

    background: #C2F2D5;
}
</style>