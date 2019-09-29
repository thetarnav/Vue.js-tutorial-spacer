<template>
  <div class="hero-image"></div>
</template>

<script>
export default {
   name: 'HeroImage',
}
</script>

<style lang="scss" scoped>
.hero-image {
   position: absolute;
   top: 0;
   left: 0;
   z-index: -1;
   width: 100%;
   height: 100vh;
   background-image: url('../assets/heroimage.jpg');
   background-size: cover;
   background-position: center;
   &::after {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      height: 100%;
      width: 100%;
      background-color: rgba(0,0,0,0.3);
   }
}
</style>