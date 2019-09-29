<template>
  <div class="claim">
     <h1>Spacer</h1>
     <p>
        Begin your journey through our amazing galaxy <br>
        and discover places never heard of.
     </p>
     <p>
        Type anything space-related to start.
     </p>
  </div>
</template>

<script>
export default {
   name: 'Claim',
}
</script>

<style lang="scss" scoped>
@import '@/scss/font-faces';
.claim {
   color: white;
   text-align: center;
   h1 {
      @include header;
   }
   p {
      @include text;
      margin-top: 15px;
   }
}

// @media (min-width: 768px) {
//    .claim {
//       p {
//          margin-top: 25px;
//       }
//    }
// }
</style>