<script>
export default {
    name: "AppCard",
    data() {
        return {

        }
    },
    components: {
    },
    methods: {
    },
    props: {
        img: String,
        name: String,
        type: String,
    }
}
</script>

<template>
    <div class="card">
        <img :src="img" alt="">
        <div class="info">
            <h4 class="tx-wt">{{ name }}</h4>
            <h5>{{ type }}</h5>
        </div>
    </div>
</template>

<style scoped>
.info {
    padding: 0.5rem;
    text-align: center;
    background-color: rgb(226, 150, 51);
}
</style>