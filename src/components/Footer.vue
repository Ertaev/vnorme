<template>
    <footer class="footer">
        <div class="container">
            <div class="footer__inner">
                <Logo class="footer__logo" />

                <p>
                    Внорме не может заменить экстренную психологическую помощь и
                    психиатрическое лечение. В случае угрожающих жизни и
                    здоровью ситуаций, необходимо обратиться по телефонам
                    доверия или в экстренную психологическую службу.
                </p>

                <div class="footer__nav">
                    <RouterLink to="/" class="footer__nav-item"
                        >Контакты</RouterLink
                    >
                    <RouterLink to="/" class="footer__nav-item"
                        >Политика конфиденциальности</RouterLink
                    >
                    <RouterLink to="/" class="footer__nav-item"
                        >Оферта</RouterLink
                    >
                    <RouterLink to="/" class="footer__nav-item"
                        >Вопросы-ответы</RouterLink
                    >
                    <RouterLink to="/" class="footer__nav-item"
                        >Стать психологом Внорме</RouterLink
                    >
                </div>
            </div>
        </div>
    </footer>
</template>

<script setup>
import Logo from "@/components/Logo.vue"
</script>

<style scoped>
.footer {
    padding: 40px 0 80px;
}

.footer__inner {
    display: flex;
    align-items: flex-start;
    gap: 40px;
}

.footer__logo {
    width: 248px;
}

.footer__inner p {
    max-width: 401px;

    font-weight: 400;
    font-size: 16px;
    line-height: 24px;

    color: #818181;
}

.footer__nav {
    display: flex;
    flex-direction: column;
    gap: 24px;

    padding-left: 40px;
}

.footer__nav-item {
    font-weight: 500;
    font-size: 16px;
    line-height: 24px;

    color: #030303;
}

@media screen and (max-width: 992px) {
    .footer__inner {
        flex-direction: column;
    }

    .footer__inner p {
        max-width: 100%;
    }

    .footer__nav {
        padding-left: 0;
    }
}
</style>
