<script setup></script>
<style lang="scss" scoped>
.wave {
  width: 100%;
  height: 110px;
  background-image: url("../assets/wave.png");
  background-size: cover;
  animation: slide-animation 5s linear infinite;
}

@keyframes slide-animation {
  0% {
    background-position: 0 0;
  }
  100% {
    background-position: -130px 0;
  }
}

@media screen and (min-width: 1564px) {
  div {
    background-size: contain;
  }
}
</style>
<template>
  <div class="wave"></div>
</template>
