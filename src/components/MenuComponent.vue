<template>
    <div class="dropdown-navbar">
        <nav class="nav-container">
            <div v-for="(menu, index) in menuItems" :key="index" class="nav-item">
                <a href="#">{{ menu.label }} ▼</a>
            </div>
        </nav>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isMobileMenuOpen: false,
            menuItems: [
                { label: 'Overview' },
                { label: 'Media' },
                { label: 'Fandom' },
                { label: 'Share' }
            ]
        };
    },
    methods: {
        toggleMobileMenu() {
            this.isMobileMenuOpen = !this.isMobileMenuOpen;
        }
    }
};
</script>

<style>
/* General Styles */
.dropdown-navbar {
    background-color: #fff;
    border-bottom: 1px solid #ddd;
    overflow-y: auto;
}

.nav-container {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
    padding: 30px 0;
}

.nav-item {
    position: relative;
}

.nav-item a {
    text-decoration: none;
    color: #000;
    font-weight: bold;
}

.nav-item:hover .dropdown {
    display: block;
}

/* Dropdown Menu (Desktop) */
.dropdown {
    display: none;
    position: absolute;
    background-color: #fff;
    border: 1px solid #ddd;
    top: 100%;
    left: 0;
    z-index: 1000;
    width: 150px;
}

.dropdown li {
    list-style: none;
}

.dropdown li a {
    display: block;
    padding: 8px 12px;
    color: #333;
}

.dropdown li a:hover {
    background-color: #f0f0f0;
}

/* Mobile Toggle Button */
.mobile-toggle {
    display: none;
    font-size: 1.5rem;
    background: none;
    border: none;
    cursor: pointer;
    padding: 10px;
}

/* Mobile Menu */
.mobile-menu {
    display: none;
    background-color: #fff;
    position: absolute;
    top: 60px;
    left: 0;
    right: 0;
    z-index: 1000;
    max-height: 80vh;
    overflow-y: auto;
    border-top: 1px solid #ddd;
    padding: 10px;
}

.mobile-nav-item {
    margin-bottom: 10px;
}

.mobile-nav-item a {
    text-decoration: none;
    color: #000;
    font-weight: bold;
}

.mobile-nav-item ul {
    margin-top: 5px;
}

.mobile-nav-item ul li a {
    font-size: 0.9rem;
    color: #555;
    display: block;
    padding: 5px 10px;
}

/* Responsive Styles */
@media (max-width: 768px) {
    .nav-container {
        overflow-y: auto;
        width: max-content;
        padding: 15px 30px;
    }

    .mobile-toggle {
        display: block;
    }

    .mobile-menu {
        display: block;
    }
}
</style>