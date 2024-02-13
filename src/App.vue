<script>
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
export default {
  name: 'App',
  data() {
    return {
    }
  },
  components: {
    AppHeader,
    AppMain
  },
  methods: {
  },
  mounted() {
  },
}
</script>

<template>
  <AppHeader></AppHeader>
  <AppMain></AppMain>
</template>

<style scoped></style>