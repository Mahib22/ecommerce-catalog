<template>
  <div class="w-full mx-auto text-center py-15 bg-img">
    <p class="py-2 font-normal text-xl">This product is unavailable to show</p>
    <slot name="nextButton"></slot>
  </div>
</template>

<style scoped>
.bg-img {
  background-image: url('../assets/img/sad-face.png');
  background-position: center;
  background-size: 80%;
  background-repeat: no-repeat;
}
</style>
