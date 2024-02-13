<script>
export default {
    name: "AppHeader",
    data() {
        return {

        }
    },
    components: {
    },
    methods: {

    },
}
</script>

<template>
    <header>
        <div class="container">
            <div class="row d-flex al-center gap-5">
                <img src="https://www.nicepng.com/png/full/71-713842_transparent-yugioh-logo-yu-gi-oh-the-art.png"
                    alt="logo">
                <span>Yu-Gi-Oh Api</span>
            </div>
        </div>
    </header>
</template>

<style scoped>
header {
    background-color: var(--ygo-light);
    padding: 1rem 0;
    font-size: 2rem;
}

img {
    width: 5rem;
}
</style>