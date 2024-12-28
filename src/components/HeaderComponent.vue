<template>
    <header class="navbar">
        <button class="hamburger" @click="toggleMenu">☰</button>
        <div class="mobile-menu" v-if="isMenuOpen">
            <a v-for="(link, index) in navLinks" :key="`mobile-${index}`" :href="link.href">{{ link.label }}</a>
            <a v-for="(action, index) in navActions" :key="`mobile-action-${index}`" :href="action.href">{{ action.label
                }}</a>
        </div>
        <div class="navbar-left">
            <div class="logo">
                <span>TMDB</span>
                <div class="logo-icon"></div>
            </div>
            <nav class="nav-links">
                <a v-for="(link, index) in navLinks" :key="index" :href="link.href">{{ link.label }}</a>
            </nav>
        </div>
        <div class="nav-actions">
            <button class="plus-btn">{{ plusSign }}</button>
            <button class="lang-btn">{{ lang }}</button>
            <a v-for="(action, index) in navActions" :key="index" :href="action.href">{{ action.label }}</a>
            <div class="search-icon">Search</div>
        </div>
        <div class="mobile-nav-right">
            <a href="#">Profile</a>
            <a href="#">Search</a>
        </div>
    </header>
</template>

<script>
export default {
    name: 'HeaderComponent',
    data() {
        return {
            plusSign: '+',
            lang: 'EN',
            isMenuOpen: false,
            navLinks: [
                { label: 'Movies', href: '#' },
                { label: 'TV Shows', href: '#' },
                { label: 'People', href: '#' },
                { label: 'More', href: '#' },
            ],
            navActions: [
                { label: 'Login', href: '#' },
                { label: 'Join TMDB', href: '#' },
            ],
        };
    },
    methods: {
        toggleMenu() {
            this.isMenuOpen = !this.isMenuOpen;
        },
    },
};
</script>

<style scoped>
/* General Styles */
.navbar {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: #032541;
    color: #fff;
    padding: 20px 30px;
}

.navbar-left {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    gap: 20px;
}

.logo {
    display: flex;
    align-items: center;
    font-size: 1.5em;
    font-weight: bold;
}

.logo-icon {
    width: 20px;
    height: 20px;
    background: #01b4e4;
    margin-left: 5px;
    border-radius: 5px;
}

.nav-links {
    display: flex;
    gap: 20px;
}

.nav-links a {
    color: #fff;
    text-decoration: none;
    font-size: 1em;
}

.nav-actions {
    display: flex;
    align-items: center;
    gap: 15px;
}

.nav-actions a {
    color: #fff;
    text-decoration: none;
}

.plus-btn {
    background: none;
    color: #fff;
    font-weight: 900;
    font-size: 1.5em;
    cursor: pointer;
    border: none;
}

.lang-btn {
    background: none;
    color: #fff;
    border: 1px solid #fff;
    padding: 5px 10px;
    cursor: pointer;
}

.search-icon {
    font-size: 1.2em;
    cursor: pointer;
}

/* Mobile Styles */
.hamburger {
    display: none;
    font-size: 1.5em;
    background: none;
    border: none;
    color: #fff;
    cursor: pointer;
}

.mobile-menu {
    display: none;
    flex-direction: column;
    background: #032541;
    position: absolute;
    top: 60px;
    right: 0;
    left: 0;
    padding: 10px;
    z-index: 1000;
}

.mobile-menu a {
    color: #fff;
    text-decoration: none;
    padding: 10px;
    text-align: center;
}

.mobile-nav-right {
    display: none;
}

.mobile-nav-right a {
    font-size: 1.2em;
    cursor: pointer;
    color: #fff;
    text-decoration: none;
    margin-left: 5px;
}

/* Responsive Design */
@media (max-width: 768px) {

    .nav-links,
    .nav-actions {
        display: none;
    }

    .hamburger {
        display: block;
    }

    .mobile-menu {
        display: flex;
    }

    .mobile-nav-right {
        display: block;
    }
}
</style>