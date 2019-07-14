<template>
  <div>

    <header-menu/>

    <div class="container-medium">
      <div class="row">
        <nuxt/>
      </div>
    </div>


  </div>
</template>
<script>
  import HeaderMenu from '../components/HeaderMenu'

  export default {
    components: { HeaderMenu },
    data() {
      return {}
    }
  }
</script>
<style lang="scss">
  h1 {
    font-size: modular-scale(3);
    line-height: 1.25;
    /*@include media-breakpoint-down(md){
      font-size: modular-scale(2);
    }*/
  }

  h2 {

  }



  p {
    font-family: $c-serif;
    letter-spacing: 0.03rem;
  }

</style>
