<script setup>
import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "./components/HelloWorld.vue";
import Header from "./components/Header.vue";
import Wave from "./components/Wave.vue";
import Lottery from "./components/Lottery.vue";
import Gift from "./components/Gift.vue";
</script>

<template>
  <Header />
  <Wave />
  <Lottery />
  <Gift />
</template>

<style scoped></style>
