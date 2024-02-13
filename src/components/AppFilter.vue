<script>
export default {
    name: "AppFilter",
    data() {
        return {

        }
    },
    components: {
    },
    methods: {
    },
    props: {
        options: Array
    }
}
</script>

<template>
    <div class="row">
        <select name="filter" id="filter">
            <option v-for="option in options" :value="option">{{ option }}</option>
        </select>
    </div>
</template>

<style scoped>
select {
    padding: 0.5rem;
    border-radius: 0.5rem;
}

.row {
    padding: 1rem 0;
}
</style>